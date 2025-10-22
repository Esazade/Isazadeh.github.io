---
layout: default
title: "Polymorphism"
parent: "ObjectOriented"
nav_order: 4
---

# Polymorphism  

Polymorphism means the ability of different types to be treated as the same base type, with behavior determined at runtime.

## Example  

```csharp
List<Shape> shapes = new List<Shape>
{
    new Circle(),
    new Shape()
};

foreach (var shape in shapes)
    shape.Draw();

//output
Drawing a circle
Drawing a shape
```
In C#, polymorphism is implemented through virtual methods and interfaces.
It’s one of the key pillars of object-oriented design that enables flexibility and reusability.