---
layout: default
title: "Encapsulation"
parent: "ObjectOriented"
nav_order: 2
---

# Encapsulation  

Encapsulation is the practice of hiding implementation details and exposing a clean interface.


## Example  

In the example below, the _balance field is private, meaning it cannot be accessed directly from outside the class.
Instead, access is controlled through a public method (Deposit) and a read-only property (Balance).

This design ensures that the internal state of the object is modified only through defined methods — keeping the data consistent and protected.  

```csharp
public class Account
{
    private decimal _balance;   // Private field

    public void Deposit(decimal amount)
    {
        _balance += amount;
    }

    public decimal Balance      // Read-only property
    {
        get { return _balance; }
    }
}
```

Encapsulation allows you to hide implementation details and expose only what’s necessary — creating cleaner, safer, and more maintainable code.