---
layout: post
title: "Blazor SSR and C# 11: Feature Adoption Guide"
excerpt: "Blazor SSR and C# 11: Feature Adoption Guide"
comments: true
categories:
  - net11
  - core
  - net
  - blazor
  - ssr
tags: 
  - blazor
  - core
  - net
  - net11
  - ssr
---

# Blazor SSR and C# 11: Feature Adoption Guide

This document outlines how we are adopting **C# 11 features** to improve our Server-Side Rendered (SSR) Blazor components. By leveraging these modern language features, we can reduce boilerplate, improve component safety, and make our markup and code-behind much cleaner.

---

## 1. Enforcing Component Parameters with `required`

Previously, ensuring that a consumer provided a necessary `[Parameter]` to a Blazor component required runtime checks, `OnInitialized` validation, or editor-only nullable warnings. C# 11 introduces the `required` modifier, which enforces initialization at compile time.

**Old Approach (Pre-C# 11):**
```csharp
@code {
    [Parameter]
    public string Title { get; set; } = default!; // Relies on runtime checks or nullable suppression
}
```

**New SSR Approach (C# 11):**
```csharp
@code {
    [Parameter]
    public required string Title { get; set; }
}
```
*Benefit:* The compiler will now guarantee that `Title` is provided when the component is instantiated, leading to safer SSR components and fewer null reference exceptions during the render tree construction.

---

## 2. Cleaner Inline Scripts and Styles with Raw String Literals

When writing SSR components, you sometimes need to output small chunks of inline JavaScript or CSS from the `@code` block. Previously, this meant dealing with messy escape characters, especially for quotes and curly braces. C# 11's raw string literals (`\"\"\"`) solve this beautifully.

**Old Approach:**
```csharp
@code {
    private string GetInlineScript() => 
        "<script>console.log(\"Hello from SSR Component\"); function log(obj) { console.log(obj); }</script>";
}
```

**New SSR Approach (C# 11):**
```csharp
@code {
    private string GetInlineScript() => \"\"\"
        <script>
            console.log("Hello from SSR Component");
            function log(obj) {
                console.log(obj);
            }
        </script>
        \"\"\";
}
```
*Benefit:* You can paste raw HTML, JS, or CSS directly into your C# variables without altering quotes or manually escaping brackets. String interpolation can also be customized by adding more `$` signs.

---

## 3. Cleaner Component Metadata via Generic Attributes

Blazor relies heavily on attributes for routing (`[Route]`), cascading values, and authorization (`[Authorize]`). If you have custom attributes for your SSR components (e.g., for metadata, layout specification, or custom SSR caching rules), C# 11 generic attributes make them strongly typed.

**New SSR Approach (C# 11):**
```csharp
// Definition
public class RequireServiceAttribute<T> : Attribute where T : class { }

// Usage in Blazor component
@attribute [RequireService<IWeatherForecastService>]

@code {
    // Component logic
}
```
*Benefit:* Avoids `typeof()` calls in attributes, making the code more readable and compile-time safe.

---

## 4. Simplified Pattern Matching with List Patterns

When processing route data, breadcrumbs, or hierarchical data in SSR components, you often need to parse arrays or lists. C# 11 List Patterns allow you to match sequences cleanly directly inside the `@code` block.

**New SSR Approach (C# 11):**
```csharp
@code {
    [Parameter] public required string[] RouteSegments { get; set; }

    protected override void OnParametersSet()
    {
        var pageType = RouteSegments switch
        {
            ["users", var userId] => $"User Profile: {userId}",
            ["users", var userId, "settings"] => $"Settings for {userId}",
            ["admin", ..] => "Admin Section",
            _ => "Unknown Route"
        };
    }
}
```
*Benefit:* Greatly simplifies complex routing or hierarchical rendering logic without writing verbose `if/else` checks.

---

## 5. File-Scoped Types for Component Helpers

Sometimes a Blazor SSR component needs a small helper DTO or class that shouldn't be exposed to the rest of the assembly. C# 11 allows `file` scoped types, which are perfect for component-specific helper structures.

```csharp
@code {
    // This class is only visible within this specific .razor file's generated class context 
    // (when using partial classes or code-behind files).
    file class ComponentState
    {
        public bool IsLoading { get; set; }
        public required string ErrorMessage { get; set; }
    }
}
```

---

## Summary of Guidelines for the Team

1. **Always** use `required` for mandatory `[Parameter]` properties.
2. **Use** raw string literals (`\"\"\"`) for any HTML/JS/CSS embedded in C# code-behind.
3. **Refactor** old `typeof(T)` attributes to use Generic Attributes where custom attributes are used.
4. **Leverage** list patterns for complex array/list data manipulation before the SSR render pass.
