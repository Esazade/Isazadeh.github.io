---
layout: default
title: "Inheritance"
parent: "ObjectOriented"
nav_order: 4
---

# Inheritance  

Inheritance allows a class to derive from another, inheriting its members and extending or overriding its behavior.

## Example  

```csharp
public class Shape
{
    public virtual void Draw() => Console.WriteLine("Drawing a shape");
}

public class Circle : Shape
{
    public override void Draw() => Console.WriteLine("Drawing a circle");
}  

Shape s = new Circle();
s.Draw();   // Output: Drawing a circle
```

Keywords to remember:  
base → access parent class members  
virtual & override → extend or redefine behavior  
sealed → prevent further inheritance  