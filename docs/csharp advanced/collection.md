---
layout: default
title: "Collections"
parent: "CsharpAdvanced"
nav_order: 1
---

# Collections  
Collections are used to store, manage, and manipulate groups of objects.  
In C#, collections can be categorized into two major types:  
- Non-generic collections: These are collections that store objects of any type.  
- Generic collections: These are collections that store objects of a specific type, providing type safety and performance improvements.

## Non-generic Collections  
Before the introduction of generics in C# 2.0, all collections were based on the System.Collections namespace, and they stored elements as object.  
Key Types:  
- ArrayList: Stores a dynamically sized collection of objects.
- Hashtable: A collection of key-value pairs, but keys and values are of type object.
- Queue / Stack: Used for FIFO (First In First Out) and LIFO (Last In First Out) operations.

```csharp
ArrayList list = new ArrayList();
list.Add(1);
list.Add("two");
list.Add(3.0);
```

## Generic Collections  
Generics provide type safety, performance improvements, and avoid the need for casting when working with collections.  
Generic collections are found in the System.Collections.Generic namespace.  

Key Types (from System.Collections.Generic):  
- List<T>: A dynamically sized collection that stores elements of type T.
- Dictionary<TKey, TValue>: A collection of key-value pairs, both key and value are of type T.
- Queue<T> / Stack<T>: Generic versions of Queue and Stack, providing type safety.

### Example of List<T>
```csharp
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        List<int> numbers = new List<int>();
        
        numbers.Add(10);
        numbers.Add(20);
        numbers.Add(30);
        
        Console.WriteLine(numbers[0]); // 10
        Console.WriteLine(numbers[1]); // 20
        
        Console.WriteLine($"Count: {numbers.Count}"); // Count: 3
        
        foreach (int num in numbers)
        {
            Console.WriteLine(num);
        }
    }
}
```
important method in list:

```csharp
List<string> fruits = new List<string>();

// Add
fruits.Add("Apple");
fruits.Add("Banana");
fruits.Add("Orange");

// Insert 
fruits.Insert(1, "Mango"); // ["Apple", "Mango", "Banana", "Orange"]

// Remove 
fruits.Remove("Banana"); // ["Apple", "Mango", "Orange"]

// RemoveAt 
fruits.RemoveAt(0); // ["Mango", "Orange"]

// Contains 
bool hasApple = fruits.Contains("Apple"); // false

// Clear 
fruits.Clear(); // []
```

### Example of Dictionary<TKey, TValue>
```csharp
Dictionary<string, string> countries = new Dictionary<string, string>();
countries.Add("IR", "Iran");
countries.Add("US", "United States");
countries.Add("TR", "Turkey");

Console.WriteLine(countries["IR"]); // Iran

if (countries.ContainsKey("US"))
{
    Console.WriteLine("US exists");
}

foreach (KeyValuePair<string, string> item in countries)
{
    Console.WriteLine($"{item.Key}: {item.Value}");
}
```

### Example of HashSet<T> 
```csharp
HashSet<int> uniqueNumbers = new HashSet<int>();
uniqueNumbers.Add(1);
uniqueNumbers.Add(2);
uniqueNumbers.Add(1); // ❌ duplicate- cannot be added

Console.WriteLine(string.Join(", ", uniqueNumbers)); // 1, 2
```

### Example of Queue<T> - (First In First Out)  
```csharp
Queue<string> queue = new Queue<string>();
queue.Enqueue("First");
queue.Enqueue("Second");
queue.Enqueue("Third");

Console.WriteLine(queue.Dequeue()); // First
Console.WriteLine(queue.Dequeue()); // Second
```

### Example of Stack<T> - (Last In First Out)
```csharp
Stack<string> stack = new Stack<string>();
stack.Push("First");
stack.Push("Second");
stack.Push("Third");

Console.WriteLine(stack.Pop()); // Third
Console.WriteLine(stack.Pop()); // Second
```
## Immutable Collections  
Immutable collections are collections that cannot be modified after they are created.  
They are part of the System.Collections.Immutable namespace.  

Key Types:  
- ImmutableList<T>: An immutable version of List<T>.
- ImmutableDictionary<TKey, TValue>: An immutable version of Dictionary<TKey, TValue>

```csharp
using System.Collections.Immutable;

var immutableList = ImmutableList<int>.Empty.Add(1).Add(2).Add(3);
Console.WriteLine(string.Join(", ", immutableList)); // 1, 2, 3

// Cannot make changes
// immutableList.Add(4); // This line will throw an error because it's immutable.

```

## Concurrent Collections  
Concurrent collections were introduced to support thread-safe operations for multi-threaded applications.  

Key Types:  
- ConcurrentQueue<T>: A thread-safe version of Queue<T>.
- ConcurrentStack<T>: A thread-safe version of Stack<T>.
- ConcurrentDictionary<TKey, TValue>: A thread-safe version of Dictionary<TKey, TValue>  

```csharp
using System.Collections.Concurrent;

ConcurrentQueue<string> queue = new ConcurrentQueue<string>();
queue.Enqueue("First");
queue.Enqueue("Second");

Console.WriteLine(queue.Dequeue()); // First
```

## Custom Collections  
If you need a specific collection, you can create your own custom collections. For this purpose, you can implement IEnumerable<T>, ICollection<T>, and IEnumerator<T>.  

```csharp
public class MyCollection<T> : ICollection<T>
{
    private List<T> _items = new List<T>();
    public int Count => _items.Count;
    public bool IsReadOnly => false;

    public void Add(T item) => _items.Add(item);
    public void Clear() => _items.Clear();
    public bool Contains(T item) => _items.Contains(item);
    public void CopyTo(T[] array, int arrayIndex) => _items.CopyTo(array, arrayIndex);
    public IEnumerator<T> GetEnumerator() => _items.GetEnumerator();
    public bool Remove(T item) => _items.Remove(item);
    IEnumerator IEnumerable.GetEnumerator() => _items.GetEnumerator();
}
```

## How to Choose the Right Collection?  
- <T>: When you need indexed access and care about maintaining order.

- <TKey, TValue>: When you need fast lookups by key.

- HashSet<T>: When uniqueness of elements is important.

- Queue<T>: When you need first-in, first-out (FIFO) processing.

- Stack<T>: When you need last-in, first-out (LIFO) behavior, such as undo/redo operations.

- Immutable Collections: When thread-safety and predictability are important.

- Concurrent Collections: When working in multi-threaded environments.