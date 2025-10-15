---
layout: default
title: "Conditions"
parent: "C#"
nav_order: 8
---

# Conditions And Loops 

Programming isn’t just about writing a few lines of code — it’s about making decisions and repeating actions when needed.  

---

## if, else if , else  
If something is true, do a certain task; otherwise, move on to the next one.

```csharp
int number = 7;

if (number % 2 == 0)
{
    Console.WriteLine("The number is even.");
}
else
{
    Console.WriteLine("The number is odd.");
}
```

```csharp
if (score >= 90)
{
    Console.WriteLine("Grade: A");
}
else if (score >= 80)
{
    Console.WriteLine("Grade: B");
}
else
{
    Console.WriteLine("Grade: F");
}
```

## switch  
A switch statement works just like a long chain of if...else if...else, but it makes your code cleaner and more readable when you need to check
multiple possible values of a single variable

```csharp
int day = 3;

switch (day)
{
    case 1:
        Console.WriteLine("Saturday");
        break;
    case 2:
        Console.WriteLine("Sunday");
        break;
    case 3:
        Console.WriteLine("Monday");
        break;
    default:
        Console.WriteLine("Invalid day");
        break;
}
```

## Important Notes About switch  
- Every case must end with a break (to exit the structure).  
- The default case works like else in an if statement — it runs when no other case matches.  
- In newer versions of C# (from version 8 onward), you can also use the switch expression for cleaner syntax.  

```csharp
int score = 85;

string grade = score switch
{
    >= 90 => "A",
    >= 80 => "B",
    >= 70 => "C",
    _ => "F"
};

Console.WriteLine("Grade: " + grade);
```

## Pattern Matching with switch  
Instead of checking only for exact values using case 1: or case "ali":, you can now use patterns such as:  
- Type patterns (checking the data type)
- Range patterns (checking numeric ranges)
- Conditional patterns using when
- Combining multiple cases  

### Type Pattern  
The program checks the type of the variable data and executes the matching case.  

```csharp
object data = "Hello";

switch (data)
{
    case int n:
        Console.WriteLine($"This is a number: {n}");
        break;

    case string s:
        Console.WriteLine($"This is a string: {s}");
        break;

    case bool b:
        Console.WriteLine($"This is a boolean value: {b}");
        break;

    default:
        Console.WriteLine("Unknown type");
        break;
}
```

### Conditional patterns using when  

```csharp
int score = 85;

switch (score)
{
    case int s when s >= 90:
        Console.WriteLine("Excellent");
        break;

    case int s when s >= 70:
        Console.WriteLine("Satisfactory");
        break;

    case int s when s < 70:
        Console.WriteLine("Needs improvement");
        break;

    default:
        Console.WriteLine("Invalid score");
        break;
}
```
