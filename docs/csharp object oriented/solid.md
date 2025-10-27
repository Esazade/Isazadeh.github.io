---
layout: default
title: "SOLID"
parent: "ObjectOriented"
nav_order: 5
---

# SOLID  
Good object-oriented design in C# follows the SOLID principles — a set of five guidelines that help keep classes small, focused, testable, and reusable.  

S - Single Responsibility Principle (SRP)

O - Open/Closed Principle (OCP)

L - Liskov Substitution Principle (LSP)

I - Interface Segregation Principle (ISP)

D - Dependency Inversion Principle (DIP)  

## S — Single Responsibility Principle  
A class should have one, and only one, reason to change.

Wrong — Multiple Responsibilities in One Class
```csharp
public class Report
{
    public void Generate() { /* Generate report */ }
    public void SaveToFile() { /* Save to file */ }
    public void EmailReport() { /* Send via email */ }
}
```
Better — Following the Single Responsibility Principle (SRP)  
```csharp
public class ReportGenerator
{
    public string Generate() => "Report content";
}

public class FileSaver
{
    public void Save(string content) { /* Save to file */ }
}

public class EmailSender
{
    public void Send(string content) { /* Send via email */ }
}
```


## O — Open/Closed Principle  
A class should be open for extension, but closed for modification. 

Wrong — Violating the Open/Closed Principle (OCP)  
```csharp
public class DiscountCalculator
{
    public double GetDiscount(string customerType)
    {
        if (customerType == "Regular") return 0.1;
        else if (customerType == "VIP") return 0.2;
        return 0;
    }
}
```
Problem:  
If you ever want to add a new customer type, you’ll have to modify this class — breaking the Open/Closed Principle.
Classes should be open for extension, but closed for modification. 

Better — Following the Open/Closed Principle
```csharp
public interface IDiscount
{
    double GetDiscount();
}

public class RegularCustomer : IDiscount
{
    public double GetDiscount() => 0.1;
}

public class VIPCustomer : IDiscount
{
    public double GetDiscount() => 0.2;
}

public class DiscountCalculator
{
    public double Calculate(IDiscount customer) => customer.GetDiscount();
}
```


## L — Liskov Substitution Principle  
Subtypes must be substitutable for their base types without altering the correctness of the program.  

Wrong — Violating the Liskov Substitution Principle (LSP)  
```csharp
public class Bird
{
    public virtual void Fly() => Console.WriteLine("Flying");
}

public class Sparrow : Bird { }

public class Penguin : Bird
{
    public override void Fly()
    {
        throw new InvalidOperationException("Penguins can’t fly!");
    }
}
```  

Better Design  
```csharp
public abstract class Bird { }

public interface IFlyingBird
{
    void Fly();
}

public class Sparrow : Bird, IFlyingBird
{
    public void Fly() => Console.WriteLine("Flying");
}

public class Penguin : Bird { }
```

## I — Interface Segregation Principle  
Clients should not be forced to depend on interfaces they do not use.  

Wrong — Violating the Interface Segregation Principle (ISP)  
```csharp
public interface IWorker
{
    void Work();
    void Eat();
}
``` 

Better Design  
```csharp
public interface IWorkable { void Work(); }
public interface IEatable { void Eat(); }

public class Human : IWorkable, IEatable
{
    public void Work() { }
    public void Eat() { }
}

public class Robot : IWorkable
{
    public void Work() { }
}
```

## D — Dependency Inversion Principle  
High-level modules should not depend on low-level modules. Both should depend on abstractions.  

Wrong — Direct Dependency  
```csharp
public class FileLogger
{
    public void Log(string msg) => File.WriteAllText("log.txt", msg);
}

public class OrderService
{
    private FileLogger _logger = new FileLogger(); // tightly coupled ❌
}
```

Better — Following the Dependency Inversion Principle (DIP)
```csharp
public interface ILogger
{
    void Log(string msg);
}

public class FileLogger : ILogger
{
    public void Log(string msg) => File.WriteAllText("log.txt", msg);
}

public class OrderService
{
    private readonly ILogger _logger;

    public OrderService(ILogger logger)
    {
        _logger = logger;
    }
}
```