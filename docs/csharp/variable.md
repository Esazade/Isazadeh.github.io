---
layout: default
title: "Variable"
parent: "C#"
nav_order: 2
---

# Variable 

A variable is like a box in memory where you store a value. 

---

## Real Example

```csharp
int age = 25;
string name = "Mehrad";

```

## Explicit Typing

Here, you’re telling the compiler exactly what type of data the variable will hold.
---

## Real Example

```csharp
int number = 10;
double price = 12.5;
float rate = 3.14f;
string name = "Sara";
bool isActive = true;

```

## Implicit Typing

You just assign the value, and C# automatically figures out what the variable’s type should be.
---

## Real Example
You can only use it when you provide an initial value, because C# needs that value to determine the variable’s type.

```csharp
var x;      // Error! No initial value provided
x = 5;

```
Keep in mind that once a variable’s type is defined, it can’t be changed later.


### When should you use var?
When the type is completely obvious from the value,But when the type might be unclear, it’s better to write it explicitly 