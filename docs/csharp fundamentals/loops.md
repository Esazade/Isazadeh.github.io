---
layout: default
title: "Loops"
parent: "Fundamentals"
nav_order: 9
---

# Loops  
When you need to run a piece of code multiple times in a row, you use a loop.  

## While Loop  
Repeats as long as the condition is true.  

```csharp
int i = 1;

while (i <= 5)
{
    Console.WriteLine(i);
    i++; // increases by 1 each time
}
```

## Do...While Loop
Runs at least once — even if the condition is false.

```csharp
int i = 1;

do
{
    Console.WriteLine(i);
    i++;
}
while (i <= 5);
```
The difference from while is that it runs the code first, and then checks the condition afterward.

## For Loop  
Used when you know exactly how many times the code should run. 

```csharp
for (int i = 0; i < 5; i++)
{
    Console.WriteLine("Hello!");
}
```

## Foreach Loop  
Used to go through (read) all the elements in an array or a list.

```csharp
string[] names = {"Ali", "Sara", "Reza"};

foreach (string name in names)
{
    Console.WriteLine(name);
}
```

# Control Statements Inside Loops  

## Break  
Used to exit a loop immediately at any point.

```csharp
for (int i = 1; i <= 10; i++)
{
    if (i == 5)
        break;

    Console.WriteLine(i);
}

// Output:
1  
2  
3  
4
```

## Continue  
Used to skip the current iteration and move to the next one.  

```csharp
for (int i = 1; i <= 5; i++)
{
    if (i == 3)
        continue; // skip number 3

    Console.WriteLine(i);
}

// Output:
1  
2  
4  
5
```