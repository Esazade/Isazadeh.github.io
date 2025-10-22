---
layout: default
title: "Abstraction"
parent: "ObjectOriented"
nav_order: 3
---

# Abstraction  

Abstraction means focusing on what an object does, rather than how it does it.  

## Example  

```csharp
public abstract class Animal
{
    public abstract void Speak();
}

public class Dog : Animal
{
    public override void Speak() => Console.WriteLine("Woof!");
}
```

The Animal class defines what every animal should do (Speak),but not how it does it.   
Each subclass, like Dog, provides its own implementation.