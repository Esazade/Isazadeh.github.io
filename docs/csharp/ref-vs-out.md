---
layout: default
title: "ref vs out"
parent: "C#"
nav_order: 6
---

# Ref 

Normally, when you pass a value (like a number) to a method, a copy of that value is sent inside the method.
But with ref and out, you can pass the actual variable itself, not just its copy.
This means the method can directly modify the original value
---

## Real Example

You have to assign an initial value to the variable before passing it to the method.

```csharp
void AddFive(ref int number)
{
    number = number + 5;
}

int a = 10;
AddFive(ref a);
Console.WriteLine(a);   // 15

```
It’s like giving someone the key to your storage room so they can go inside and change something themselves 😊


## Out 

Here, you don’t need to assign an initial value, because the method itself will provide one.
---

## Real Example

```csharp
void GetSumAndProduct(int x, int y, out int sum, out int product)
{
    sum = x + y;
    product = x * y;
}

int s, p;   // without an initial value
GetSumAndProduct(3, 4, out s, out p);
Console.WriteLine($"Sum = {s}, Product = {p}");

```
It’s like handing someone an empty box and saying,
“Fill this up for me and bring it back.” 


