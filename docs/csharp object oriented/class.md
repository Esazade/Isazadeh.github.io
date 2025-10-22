---
layout: default
title: "Class"
parent: "ObjectOriented"
nav_order: 1
---

# Class 

A class is like a blueprint or template for creating objects.

---

## Creating a Class

```csharp
public class Car
{
}
```

## Adding State and Behavior

A class usually has two main parts:  

- Fields → store data or state

- Methods → perform actions or define behavior

## Defining a Field  

A field is simply a variable declared inside a class that holds data.  
```csharp
public class Car
{
    public string brand;
    public int speed;
}
```

## Defining a Method
  
A method represents an action that an object can perform — for example, driving or stopping.  
```csharp
public class Car
{
    public string brand;
    public int speed;

    public void Drive()
    {
        Console.WriteLine(brand + " is driving at " + speed + " km/h");
    }

    public void Stop()
    {
        Console.WriteLine(brand + " stopped!");
    }
}
```
The keyword void means this method doesn’t return any value.

## Creating an Object from a Class
  
To use a class, you need to create an object (an instance of that class)   
```csharp
Car myCar = new Car();

myCar.brand = "BMW";
myCar.speed = 120;
myCar.Drive();
```

## Adding a Constructor
  
A constructor is a special method that runs automatically when an object is created.  
```csharp
public class Car
{
    public string brand;
    public int speed;

    // Constructor
    public Car()
    {
        brand = "Unknown";
        speed = 0;
    }
}

Car myCar = new Car();
Console.WriteLine(myCar.brand); // Unknown
```

## Constructor with Parameters
  
You can create a constructor that takes values from the user when an object is created  
```csharp
public class Car
{
    public string brand;
    public int speed;

    // Constructor with parameters
    public Car(string carBrand, int carSpeed)
    {
        brand = carBrand;
        speed = carSpeed;
    }

    public void Drive()
    {
        Console.WriteLine(brand + " is driving at " + speed + " km/h");
    }
}

Car car1 = new Car("Toyota", 100);
Car car2 = new Car("BMW", 180);

car1.Drive();       // Toyota is driving at 100 km/h
car2.Drive();       // BMW is driving at 180 km/h
```

## Working with Static Members
  
Static members belong to the class itself, not to any specific object.  

```csharp
public class Car
{
    public string brand;
    public int speed;
    public static int count = 0; // static field

    public Car(string carBrand, int carSpeed)
    {
        brand = carBrand;
        speed = carSpeed;
        count++; // increases each time a new car is created
    }
}

Car car1 = new Car("BMW", 120);
Car car2 = new Car("Audi", 140);
Console.WriteLine("Total cars: " + Car.count);      // Total cars: 2
```

## Using Getters and Setters  
In C#, *properties* let you control how fields are read or updated.  
They use **getters** (for reading values) and **setters** (for assigning values).

Instead of using public fields like this:
```csharp
public class Car
{
    public string brand;
    public int speed;
}
```   
You can use properties to protect the data:
```csharp
public class Car
{
    private string brand;  // private field

    public string Brand    // Property
    {
        get { return brand; }              // Getter
        set { brand = value; }             // Setter
    }
}
```
Now you can access the property safely:  
```csharp
Car myCar = new Car();
myCar.Brand = "BMW";          // calls the setter
Console.WriteLine(myCar.Brand); // calls the getter
``` 
## Adding Validation  
You can add logic inside the setter to validate data before saving it.
```csharp
public class Car
{
    private int speed;

    public int Speed
    {
        get { return speed; }
        set
        {
            if (value < 0)
                throw new ArgumentException("Speed cannot be negative!");
            speed = value;
        }
    }
}
```

## Auto-Implemented Properties  
If you don’t need any extra logic, you can let C# automatically create a hidden field:
```csharp
public class Car
{
    public string Brand { get; set; }
    public int Speed { get; set; }
}
``` 
This is the same as manually writing a field with a basic getter and setter.

## Read-Only and Write-Only Properties  
You can also make a property read-only (getter only) or write-only (setter only):
```csharp
public class Car
{
    public string Model { get; } = "Sedan";  // read-only
    public string Password { private get; set; }  // write-only from outside
}
``` 