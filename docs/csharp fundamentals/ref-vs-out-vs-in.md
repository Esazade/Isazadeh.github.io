---
layout: default
title: "ref vs out vs in"
parent: "Fundamentals"
nav_order: 7
---

# ref vs out vs in
Normally, when you pass a value (like a number) to a method, a copy of that value is passed inside the method.  
However, with the keywords ref, out, and in, you can pass a variable by reference — meaning the method receives a direct reference to the original variable rather than a copy.  
- With ref and out, the method can modify the original variable.
- With in, the method can read the original variable without creating a copy, but cannot modify it. 


## How ref Works

When using **ref**, the variable **must be initialized** before passing it to the method.  
The method can then **read and modify** the value.


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


## How out Works 
When using out, the variable doesn’t need an initial value.  
The method must assign a value to it before it returns.


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

## How in Works  
The in keyword was introduced in C# 7.2. It also passes arguments by reference, but with one key difference:  
You can read the value inside the method, but you cannot modify it.  
So, it avoids copying large structures (like struct) while still ensuring read-only safety.

```csharp
void PrintPoint(in Point p)
{
    // p.X = 10; ❌ Error: cannot modify because it's passed as 'in'
    Console.WriteLine($"X = {p.X}, Y = {p.Y}");
}

struct Point
{
    public int X;
    public int Y;
}

Point myPoint = new Point { X = 5, Y = 7 };
PrintPoint(in myPoint);  // Pass by reference, but read-only
```
Think of in like giving someone a photo of your document to read — they can see it, but not edit it

