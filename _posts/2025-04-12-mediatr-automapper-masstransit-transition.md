---
layout: post
title: "Mediatr Automapper MassTransit Transition"
excerpt: "Mediatr Automapper MassTransit Transition"
comments: true
categories:
  - .net core
  - oss
tags: 
  - .net core
---

# Mediatr Automapper MassTransit Transition

- Switch to alternatives
  - For AutoMapper: consider Mapster or manual mapping (my recommendation).  
  - For MediatR: explore FastEndpoints or build a simple mediator yourself.  
  - For MassTransit: look at raw client libraries like RabbitMQ.Client and Azure.Messaging.ServiceBus, and another option to consider is Rebus.
- Write equivalent functionality yourself
  - MediatR isn't too complex to build on your own. I recommend giving it a try as an excellent coding exercise - it's probably the simplest way to move away from MediatR.
  - For AutoMapper, many teams have deep integrations with business logic in custom mappers. This makes extracting and replacing it difficult. Expect significant tech debt if you don't address this.
  - MassTransit, on the other hand, does so many things (and does them well) that migrating away would be challenging. Saga support or the request-response messaging features are hard to replicate. The only real alternative is diving into raw client libraries for your chosen message transport.
