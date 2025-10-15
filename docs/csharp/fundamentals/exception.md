---
layout: default
title: "Exception"
parent: "fundamentals"
nav_order: 10
---

# Exception  
An exception is an unexpected event that occurs during program execution. Examples include:  
- Division by zero
- Opening a file that doesn’t exist  
When this happens, C# throws an exception, and if you “catch” it using try...catch,you can prevent your program from crashing.  

## Common Exception Types in C#

| Exception Type              | Meaning                                      |
|-----------------------------|----------------------------------------------|
| DivideByZeroException       | Division by zero                             |
| NullReferenceException      | Trying to access a null object               |
| IndexOutOfRangeException    | Index is outside the array or list range     |
| FormatException             | Invalid type conversion (e.g., string → int) |
| FileNotFoundException       | File not found                               |
| InvalidOperationException   | Invalid operation in the current state       |

```csharp
int a = 5;
int b = 0;

try
{
    int result = a / b;
    Console.WriteLine(result);
}
catch (DivideByZeroException ex)
{
    Console.WriteLine("You can't divide a number by zero!");
}
```

## finally Block  
The code inside finally always runs — whether or not an exception occurs  

```csharp
try
{
    int x = 10 / 0;
}
catch
{
    Console.WriteLine("An error occurred!");
}
finally
{
    Console.WriteLine("Program finished.");
}
```

## Throwing Exceptions Manually  
Sometimes you may want to throw an exception yourself to signal that something went wrong.  

```csharp
static void CheckAge(int age)
{
    if (age < 18)
        throw new Exception("❌ Age must be at least 18!");
    else
        Console.WriteLine("✅ Access granted.");
}

static void Main()
{
    try
    {
        CheckAge(15);
    }
    catch (Exception ex)
    {
        Console.WriteLine(ex.Message);
    }
}
```

### Pro Tips  
- Always catch specific exceptions instead of the general Exception.
- For large projects, define your custom exception classes.  
- In production, log exceptions instead of displaying them directly.
