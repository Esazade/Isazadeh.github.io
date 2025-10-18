---
layout: default
title: "List"
parent: "Fundamentals"
nav_order: 4
---

# List 

A List is similar to an array — it’s a collection of elements of the same type. But the difference is that its size isn’t fixed!  
You can add or remove items from a list at any time
---

## Defining a List
To use a List, you need to include the following namespace:
```csharp
using System.Collections.Generic;

```
Then, create a new list
```csharp
List<int> numbers = new List<int>();
```

## Adding Items to a List
```csharp
numbers.Add(10);
numbers.Add(20);
numbers.Add(30);
```
Now, the numbers list contains [10, 20, 30].

## Accessing List Elements
Just like arrays, you can access items in a list using their index:

```csharp
Console.WriteLine(numbers[0]); // Output: 10
numbers[1] = 25;               // Change the value of the second element
```
### Removing Items from a List

#### By Value:
```csharp
numbers.Remove(25); // removes the number 25
```
#### By Index:
```csharp
numbers.RemoveAt(0); // removes the first element
```

## Counting Elements
You can find out how many items are currently in the list using Count:

```csharp
Console.WriteLine(numbers.Count);
```
## Looping Through a List

### Using foreach
```csharp
foreach (int n in numbers)
{
    Console.WriteLine(n);
}
```
### Using for
```csharp
for (int i = 0; i < numbers.Count; i++)
{
    Console.WriteLine(numbers[i]);
}
```