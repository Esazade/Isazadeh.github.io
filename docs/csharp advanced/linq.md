---
layout: default
title: "LINQ"
parent: "CsharpAdvanced"
nav_order: 1
---

# LINQ  
LINQ (Language Integrated Query) is a set of language and framework features that bring query capabilities into C#.  
LINQ queries work on any data source that supports a suitable provider.  
Common providers include:
- LINQ to Objects – for in-memory collections (List<T>, Array, etc.)
- LINQ to XML – for XML documents (XDocument, XElement)
- LINQ to Entities – for querying databases through Entity Framework
- LINQ to DataSet – for ADO.NET DataSets

## Query Syntax vs Method Syntax  
C# supports two syntaxes for writing LINQ queries:  
- Query syntax (SQL-like)
- Method syntax (fluent chain of extension methods)

### Query Syntax Example
```csharp
var result = from n in numbers
             where n > 2
             orderby n descending
             select n;
```

### Method Syntax Example
```csharp
var result = numbers
    .Where(n => n > 2)
    .OrderByDescending(n => n);
```

## LINQ Operators

### Where  
Filters elements in a sequence based on a specified condition.
```csharp
// Query Syntax
var filtered = from num in numbers
               where num > 5
               select num;

// Method Syntax
var filtered = numbers.Where(num => num > 5);
```

### OfType  
Filters elements in a sequence to include only those of a specified type.

```csharp
object[] mixedArray = { 1, "hello", 2, "world", 3.14 };
var strings = mixedArray.OfType<string>(); // ["hello", "world"]
```

### OrderBy / OrderByDescending  
These are used to sort a collection by a specified key in ascending or descending order.

```csharp
var sortedAsc = students.OrderBy(s => s.Age);
var sortedDesc = students.OrderByDescending(s => s.Age);
```

### ThenBy / ThenByDescending  
These are are used for secondary sorting when multiple sort criteria are applied.

```csharp
var sorted = students.OrderBy(s => s.LastName)
                     .ThenBy(s => s.FirstName);
```

### GroupBy  
GroupBy in LINQ groups elements in a collection based on a specified key.

```csharp
var words = new[] { "apple", "banana", "apricot", "blueberry" };
var groups = words.GroupBy(w => w[0]);

foreach (var g in groups)
    Console.WriteLine($"{g.Key}: {string.Join(", ", g)}");

// output
a: apple, apricot  
b: banana, blueberry
```

### First / FirstOrDefault  
First() gets the first matching element and throws an error if none found.
FirstOrDefault() safely returns the first matching element or a default value if none exists.

```csharp
var numbers = new int[] { 1, 2, 3 };
var first = numbers.FirstOrDefault(); // 1

var empty = new int[] { };
var safe = empty.FirstOrDefault();    // 0 (default of int)
```

### Join / Group Join
join in LINQ combines two collections based on a matching key (like an SQL INNER JOIN), while group join groups related elements from the second collection into each element of the first (like an SQL LEFT JOIN).

```csharp
var students = new[]
{
    new { Name = "Ali", ClassId = 1 },
    new { Name = "Sara", ClassId = 2 }
};

var classes = new[]
{
    new { ClassId = 1, Title = "Math" },
    new { ClassId = 2, Title = "Physics" }
};

// join
var joinResult = from s in students
                 join c in classes on s.ClassId equals c.ClassId
                 select new { s.Name, c.Title };

// group join
var groupJoinResult = from c in classes
                      join s in students on c.ClassId equals s.ClassId into studentGroup
                      select new { c.Title, Students = studentGroup };
```

### Concat / Distinct
Concat() joins two sequences end-to-end without removing duplicates, while Distinct() returns only unique elements from a sequence.

```csharp
var list1 = new[] { 1, 2, 3 };
var list2 = new[] { 3, 4, 5 };

var result = list1.Concat(list2).Distinct();
Console.WriteLine(string.Join(", ", result)); // 1, 2, 3, 4, 5
```

### Zip  
Zip() combines two sequences element by element into a single sequence of pairs (or any custom result you define).

```csharp
var names = new[] { "Ali", "Sara", "Nima" };
var scores = new[] { 90, 85, 95 };

var students = names.Zip(scores, (name, score) => new { name, score });

foreach (var s in students)
    Console.WriteLine($"{s.name}: {s.score}");
```

### Skip / Take  
Skip() ignores a number of elements from the start, and Take() returns a limited number of elements — together they’re perfect for paging or slicing sequences.

```csharp
var numbers = Enumerable.Range(1, 10); // [1,2,3,4,5,6,7,8,9,10]

var skipped = numbers.Skip(5); // Skips first 5 elements
var taken = numbers.Take(5);   // Takes first 5 elements

Console.WriteLine("Skip(5): " + string.Join(", ", skipped));
Console.WriteLine("Take(5): " + string.Join(", ", taken));

//Output
Skip(5): 6, 7, 8, 9, 10
Take(5): 1, 2, 3, 4, 5
```

### TakeWhile / SkipWhile  
Takes elements from the start of a sequence as long as the condition is true. Stops when it becomes false.  
Skips elements from the start of a sequence as long as the condition is true, and then takes the rest.

```csharp
var numbers = new[] { 1, 2, 3, 7, 8, 9 };
var result = numbers.TakeWhile(n => n < 5);
Console.WriteLine(string.Join(", ", result));

//Output
1, 2, 3
```

```csharp
var numbers = new[] { 1, 2, 3, 7, 8, 9 };
var result = numbers.SkipWhile(n => n < 5);
Console.WriteLine(string.Join(", ", result));

//Output
7, 8, 9
```