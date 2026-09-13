---
layout: post
title: "Comprehensive Guide: .NET 11 Automatic CSRF Protection Across All Blazor Render Modes"
excerpt: "Comprehensive Guide: .NET 11 Automatic CSRF Protection Across All Blazor Render Modes"
comments: true
categories:
  - net11
  - core
  - net
  - blazor
  - crrf
  - security
  - owasp
tags: 
  - blazor
  - core
  - net
  - net11
  - crrf
  - security
  - owasp
---

# Comprehensive Guide: .NET 11 Automatic CSRF Protection Across All Blazor Render Modes

.NET 11 introduces a **Fetch Metadata-based automatic CSRF protection mechanism** built directly into ASP.NET Core pipelines. Replacing traditional cryptographic synchronizer tokens (`__RequestVerificationToken`) and heavy server-side Data Protection validation, the new `CsrfProtectionMiddleware` automatically validates browser-managed headers (`Sec-Fetch-Site`, `Sec-Fetch-Mode`, and `Origin`) across all Blazor project templates.

---

## 1. Core Architectural Shift

| Architectural Aspect | Traditional Token Model (.NET 8/9/10) | .NET 11 Automatic CSRF |
| :--- | :--- | :--- |
| **Validation Mechanism** | Cryptographic token matching in form payload/cookies | Browser-managed Fetch Metadata header evaluation |
| **State & Cryptography** | Requires Data Protection keys, server state, per-request encryption | Zero cryptographic overhead (pure header evaluation) |
| **Multi-Tab Reliability** | Prone to token race conditions and invalidations across tabs | Seamless execution across multiple tabs |
| **Middleware Pipeline** | Required explicit `app.UseAntiforgery()` and component attributes | Enabled automatically via `WebApplication.CreateBuilder` |
| **Non-Browser Callers** | Required token suppression or custom validation rules | Automatically allowed (missing Fetch Metadata headers) |

---

## 2. The 5-Rule Evaluation Algorithm

The `CsrfProtectionMiddleware` evaluates incoming requests early in the pipeline using a deterministic, 5-step decision hierarchy:

1. **Safe HTTP Verbs:** `GET`, `HEAD`, `OPTIONS`, and `TRACE` are permitted unconditionally (RFC 9110 §9.2.1).
2. **Same-Origin & Direct Navigations:** Requests where `Sec-Fetch-Site` is `same-origin` or `none` (user typed URL, clicked bookmark, or navigated same-site) are allowed.
3. **CORS-Approved Origins:** Cross-origin requests with an `Origin` header matching the endpoint's configured CORS policy are allowed.
4. **Non-Browser Clients:** Requests lacking both `Sec-Fetch-Site` and `Origin` headers (e.g., cURL, Postman, mobile native SDKs, server-to-server callers) pass through, as CSRF is strictly a browser-based attack vector.
5. **Unsafe Cross-Site Requests:** Any remaining request (e.g., cross-site `POST`, `PUT`, `DELETE`, `PATCH` missing explicit CORS approval) is marked invalid and rejected with an **HTTP 400 Bad Request**.

---

## 3. Impact Across All Blazor Render Modes

### Static Server-Side Rendering (Static SSR)
- **Standard Forms:** Plain HTML `<form action="..." method="post">` submissions within static components no longer require hidden token fields or `@attribute [RequireAntiforgeryToken]`.
- **Automatic Form Validation:** The form mapping infrastructure checks `IAntiforgeryValidationFeature` deferred state. Same-origin form posts succeed automatically.

### Interactive Server (SignalR)
- **Initial Connection Handshake:** The initial HTTP negotiation request (`/blazor/negotiate`) is evaluated by the CSRF middleware. Because it originates from the app's same origin, it passes automatically.
- **WebSocket Upgrade:** Once established, WebSocket frames transmit state directly without additional CSRF overhead.

### Interactive WebAssembly (Blazor WASM)
- **Hosted WASM (Same-Origin):** When hosted ASP.NET Core apps serve the Blazor WASM client on the same domain/port, all `HttpClient` calls send `Sec-Fetch-Site: same-origin` and require zero special configuration.
- **Standalone WASM (Cross-Origin APIs):** If the client runs on `https://app.example.com` and communicates with `https://api.example.com`:
  - Cross-origin `POST`/`PUT`/`DELETE` calls will be blocked by default.
  - **Solution:** Configure a default CORS policy on the API backend to trust the client origin, or adopt a **Backend-for-Frontend (BFF)** reverse proxy pattern.

### Interactive Auto Mode (SSR + WebAssembly/Server)
- **Pre-rendering to Interactivity Transition:** Handles state transition without token mismatch errors. Whether the request is an initial SSR form submit or a client-side fetch, same-origin Fetch Metadata headers guarantee validation.

### Blazor Hybrid (MAUI & Desktop WebViews)
- **WebView Behavior:** Native WebViews (MAUI Blazor, Capacitor) may emit `Sec-Fetch-Site: none` or omit headers entirely depending on the OS platform.
- **Validation outcome:** Missing headers pass through under Rule 4 (Non-Browser), ensuring native desktop and mobile hybrid apps continue working cleanly.

---

## 4. Endpoints & Exemption Strategies

### Exempting Third-Party Callbacks & Webhooks
Third-party providers (e.g., Stripe webhooks, Entra ID / OAuth `form_post` logins) send cross-origin `POST` requests to your app without CORS headers. These specific endpoints must opt out of CSRF protection:

#### Minimal API Endpoints:
```csharp
app.MapPost("/api/webhooks/stripe", () => Results.Ok())
   .DisableAntiforgery();
```

#### Razor Components & Controller Actions:
```csharp
@attribute [IgnoreAntiforgeryToken]
```

### CORS Trust Configuration for SPAs & WASM
To permit cross-origin requests from trusted frontends without disabling CSRF globally:

```csharp
builder.Services.AddCors(options =>
{
    options.AddDefaultPolicy(policy =>
    {
        policy.WithOrigins("https://my-blazor-wasm-app.com")
              .AllowAnyHeader()
              .AllowAnyMethod();
    });
});
```

---

## 5. Development & Testing Recommendations

1. **Avoid `HttpClient` Only Tests for Security Automation:** Automated integration tests using raw `HttpClient` do not emit browser `Sec-Fetch-Site` headers and will pass through Rule 4. Test browser authentication flows using Playwright or Selenium.
2. **Dev Server Proxying:** In multi-project solutions where the WASM client dev server runs on `localhost:5001` and the API on `localhost:7001`, configure launch settings or reverse proxies to avoid cross-origin dev breakage.
3. **Diagnostic Opt-Out:** If unexpected 400 errors occur during migration, set `DisableCsrfProtection` in app configuration as a temporary diagnostic step to isolate whether CSRF middleware is the cause.
