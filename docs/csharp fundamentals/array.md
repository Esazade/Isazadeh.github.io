---
layout: default
title: "Array"
parent: "Fundamentals"
nav_order: 3
---

# Array 

An array is like a big box divided into smaller compartments and in each compartment, you can store a value of the same data type

---

## How to Define an Array

### Method 1: Define with Initial Values
```csharp
int[] numbers = { 1, 2, 3, 4, 5 };
```

### Method 2: Define with a Fixed Size
```csharp
int[] ages = new int[3];    // array with 3 elements
ages[0] = 20;
ages[1] = 25;
ages[2] = 30;
```

## Iterating Through an Array (Loop)
To read all the values of an array, you usually use either a for loop or a foreach loop.

### Using for
```csharp
for (int i = 0; i < scores.Length; i++)
{
    Console.WriteLine(scores[i]);
}
```

### Using foreach
```csharp
foreach (int score in scores)
{
    Console.WriteLine(score);
}
```
Both loops go through all elements of the array

## Types of Arrays in C#

### One-Dimensional Array (Simple Array)
```csharp
int[] numbers = { 1, 2, 3 };
```

### Two-Dimensional Array (Like a Table)
```csharp
int[,] matrix = {
    { 1, 2, 3 },
    { 4, 5, 6 }
};

Console.WriteLine(matrix[1, 2]); // Output: 6
```

### Multidimensional Array (3D or more)
```csharp
int[,,] cube = {
    {
        { 1, 2 },
        { 3, 4 }
    },
    {
        { 5, 6 },
        { 7, 8 }
    }
};

Console.WriteLine(cube[1, 0, 1]); // Output: 6
```

### Jagged Array (Array of Arrays)
Think of it like shelves with rows of different lengths — each row can store a different number of items.

```csharp
int[][] numbers = new int[3][];
numbers[0] = new int[] { 1, 2, 3 };
numbers[1] = new int[] { 4, 5 };
numbers[2] = new int[] { 6, 7, 8, 9 };

Console.WriteLine(numbers[1][0]); // Output: 4
```

### Array of Objects
```csharp
Book[] books = new Book[2];
books[0] = new Book("C# Basics");
books[1] = new Book("Advanced C#");

Console.WriteLine(books[0].Title); // Output: C# Basics
```

### Implicitly Typed Array
```csharp
var names = new[] { "Sara", "Ali", "Reza" };  // string[]
var numbers = new[] { 1, 2, 3, 4 };           // int[]
```