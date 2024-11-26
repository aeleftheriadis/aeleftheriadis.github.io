---
layout: post
title: "Chain Responsibility Pattern in C#"
excerpt: "Chain Responsibility Pattern in C#"
comments: true
categories:
  - .Net
tags: 
  - .net
  - architecture
---


# Chain Responsibility Pattern in C#

## The Background

The **Chain of Responsibility pattern** is a behavioral design pattern that allows you to build a chain of objects to handle a request or perform a task. Each object in the chain has the ability to either handle the request or pass it on to the next object in the chain. This pattern promotes loose coupling and flexibility in handling requests.

Let's explore how to implement the **Chain of Responsibility pattern** in .NET 6 using a practical example.

## Example Scenario

Let's consider a scenario where we have a series of discount rules for an e-commerce application. Depending on the customer's profile, we want to apply different discount percentages to their orders.

The discount rules are as follows:
- If the customer is a **VIP**, apply a **20% discount**.
- If the customer is a **regular customer**, apply a **10% discount**.
- If the customer is a **new customer**, apply a **5% discount**.
- If none of the above rules match, apply **no discount**.

Initially, we can handle this logic using a series of If statements:

```csharp
public decimal CalculateDiscount(Customer customer, decimal orderTotal)
{
    if (customer.IsVIP)
    {
        return orderTotal * 0.8m; // 20% discount
    }
    else if (customer.IsRegular)
    {
        return orderTotal * 0.9m; // 10% discount
    }
    else if (customer.IsNew)
    {
        return orderTotal * 0.95m; // 5% discount
    }
    else
    {
        return orderTotal; // no discount
    }
}
```

it's not correct
I apologize for that. Let's correct it. Here's the text with strong emphasis (bold) in markdown:

markdown
# Chain Responsibility Pattern in C#

## The Background

The **Chain of Responsibility pattern** is a behavioral design pattern that allows you to build a chain of objects to handle a request or perform a task. Each object in the chain has the ability to either handle the request or pass it on to the next object in the chain. This pattern promotes loose coupling and flexibility in handling requests.

Let's explore how to implement the **Chain of Responsibility pattern** in .NET 6 using a practical example.

## Example Scenario

Let's consider a scenario where we have a series of discount rules for an e-commerce application. Depending on the customer's profile, we want to apply different discount percentages to their orders.

The discount rules are as follows:
- If the customer is a **VIP**, apply a **20% discount**.
- If the customer is a **regular customer**, apply a **10% discount**.
- If the customer is a **new customer**, apply a **5% discount**.
- If none of the above rules match, apply **no discount**.

Initially, we can handle this logic using a series of If statements:

```csharp
public decimal CalculateDiscount(Customer customer, decimal orderTotal)
{
    if (customer.IsVIP)
    {
        return orderTotal * 0.8m; // 20% discount
    }
    else if (customer.IsRegular)
    {
        return orderTotal * 0.9m; // 10% discount
    }
    else if (customer.IsNew)
    {
        return orderTotal * 0.95m; // 5% discount
    }
    else
    {
        return orderTotal; // no discount
    }
}
```

## Chain of Responsibility
While the If statements approach works, it can become unwieldy when the number of rules grows. The Chain of Responsibility pattern provides a more flexible and maintainable solution.

Let's refactor the code to use this pattern.

**Step #1**: Create an **abstract handler class, DiscountHandler**, that defines a common interface for all discount handlers:

```csharp
public abstract class DiscountHandler
{
    protected DiscountHandler _nextHandler;

    public void SetNextHandler(DiscountHandler nextHandler)
    {
        _nextHandler = nextHandler;
    }

    public abstract decimal CalculateDiscount(Customer customer, decimal orderTotal);
}
```

**Step #2**: Implement **concrete discount handlers** by deriving from DiscountHandler. Each handler will handle a specific rule and decide whether to apply a discount or pass the request to the next handler.

**VIPDiscountHandler**:
```csharp
public class VIPDiscountHandler : DiscountHandler
{
    public override decimal CalculateDiscount(Customer customer, decimal orderTotal)
    {
        if (customer.IsVIP)
        {
            return orderTotal * 0.8m; // 20% discount
        }
        return _nextHandler?.CalculateDiscount(customer, orderTotal) ?? orderTotal;
    }
}
```

**RegularDiscountHandler**:
```csharp
public class RegularDiscountHandler : DiscountHandler
{
    public override decimal CalculateDiscount(Customer customer, decimal orderTotal)
    {
        if (customer.IsRegular)
        {
            return orderTotal * 0.9m; // 10% discount
        }
        return _nextHandler?.CalculateDiscount(customer, orderTotal) ?? orderTotal;
    }
}
```

**NewCustomerDiscountHandler**:
```csharp
public class NewCustomerDiscountHandler : DiscountHandler
{
    public override decimal CalculateDiscount(Customer customer, decimal orderTotal)
    {
        if (customer.IsNew)
        {
            return orderTotal * 0.95m; // 5% discount
        }
        return _nextHandler?.CalculateDiscount(customer, orderTotal) ?? orderTotal;
    }
}
```
**NoDiscountHandler**:
```csharp
public class NoDiscountHandler : DiscountHandler
{
    public override decimal CalculateDiscount(Customer customer, decimal orderTotal)
    {
        return orderTotal; // no discount
    }
}
```
**Step #3**: With the concrete handlers in place, we can create the chain by linking them together:
```csharp
var vipHandler = new VIPDiscountHandler();
vipHandler.SetNextHandler(new RegularDiscountHandler())
          .SetNextHandler(new NewCustomerDiscountHandler())
          .SetNextHandler(new NoDiscountHandler());
```
Finally, we can invoke the chain by calling the **CalculateDiscount** method on the first handler in the chain:

```csharp
decimal discountAmount = vipHandler.CalculateDiscount(customer, orderTotal);
```
## Pros and Cons
What are the benefits from this?

1. **Flexibility**

The Chain of Responsibility pattern allows you to dynamically modify or extend the chain without affecting other parts of the code. You can add or remove handlers as needed.

2. **Loose coupling**

The pattern promotes loose coupling between the sender of a request and its receivers. Each handler only needs to know about its immediate successor, minimizing dependencies. 

3. **Single Responsibility Principle**

You can decouple classes that invoke operations from classes that perform operations.

Okay,what about Drawbacks?

1. **Request may go unhandled**

If none of the handlers in the chain can handle the request, it may go unhandled, leading to unexpected behavior. It's important to have a default handler or a way to handle such scenarios.

2. **Potential performance impact**

If the chain becomes very long, it may result in performance overhead due to the traversal of multiple handlers.

## Wrapping Up

The Chain of Responsibility pattern offers an elegant way to manage complex workflows by decoupling the sender and receiver of a request. Whether you're designing systems that involve validation, logging, or dynamic decision-making, this pattern can simplify your architecture while keeping it flexible and maintainable.

By breaking down responsibilities into discrete handlers, you gain the ability to reuse components, extend functionality with minimal effort, and maintain a cleaner separation of concerns. As we've seen through the examples, implementing this pattern in a real-world .NET application can enhance your system’s scalability and adaptability.

Now that you’ve grasped the essence of the Chain of Responsibility, consider how it might fit into your own projects. Could it help streamline your logging pipelines, enhance error-handling mechanisms, or build a powerful middleware architecture? 

The next time you find yourself creating tightly coupled workflows, let the Chain of Responsibility inspire you to design smarter, more adaptable solutions.

[Original Article](https://thecodeman.net/posts/chain-responsibility-pattern)