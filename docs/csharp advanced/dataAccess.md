---
layout: default
title: "Data Access"
parent: "CsharpAdvanced"
nav_order: 4
---

# What is Data Access?  

Data access refers to connecting to, querying and manipulating data stored in a persistent storage system — typically a relational database.  
In .NET, data access can be performed through low-level APIs such as ADO.NET or high-level frameworks such as Entity Framework Core (EF Core). 

## ADO.NET — The Core of Data Access  
ADO.NET is the foundational .NET API for communicating with relational databases.  
It provides classes for establishing connections, executing commands, and reading or writing data.

### Key ADO.NET Classes  

| Description                                        | Class                     |
|----------------------------------------------------|---------------------------|
| Opens a connection to a SQL Server database        | `SqlConnection`           |
| Executes SQL statements or stored procedures       | `SqlCommand`              |
| Provides a fast, forward-only way to read data     | `SqlDataReader`           |
| Bridges between DataSet and the database           | `SqlDataAdapter`          |
| In-memory representation of relational data        | `DataSet` / `DataTable`   |

#### Example: Reading Data  
```csharp
using System.Data.SqlClient;

string connectionString =
    "Data Source=.;Initial Catalog=ShopDB;Integrated Security=True";

using (SqlConnection conn = new SqlConnection(connectionString))
{
    conn.Open();
    string query = "SELECT Id, Name, Price FROM Products";

    SqlCommand cmd = new SqlCommand(query, conn);
    SqlDataReader reader = cmd.ExecuteReader();

    while (reader.Read())
    {
        Console.WriteLine($"{reader["Id"]}: {reader["Name"]} - {reader["Price"]}");
    }
}
```

#### Example: Inserting Data  
```csharp
string insertQuery = "INSERT INTO Products (Name, Price) VALUES (@n, @p)";
using (SqlCommand cmd = new SqlCommand(insertQuery, conn))
{
    cmd.Parameters.AddWithValue("@n", "Keyboard");
    cmd.Parameters.AddWithValue("@p", 99.99);
    cmd.ExecuteNonQuery();
}
```

## Entity Framework Core (EF Core) — Modern Data Access  
Entity Framework Core (EF Core) is Microsoft’s modern Object–Relational Mapper (ORM).  
It allows developers to work with data using C# objects instead of raw SQL.  

### EF Core Key Concepts

| Description                                       | Concept        |
|---------------------------------------------------|----------------|
| Represents a session with the database            | `DbContext`    |
| Represents a table of entities                    | `DbSet<T>`     |
| A C# class mapped to a database table             | Model Class    |
| Allows querying data in an object-oriented way    | LINQ Query     |


#### Example: Basic EF Core Model   
```csharp
using Microsoft.EntityFrameworkCore;

public class Product
{
    public int Id { get; set; }
    public string Name { get; set; } = "";
    public decimal Price { get; set; }
}

public class ShopContext : DbContext
{
    public DbSet<Product> Products => Set<Product>();

    protected override void OnConfiguring(DbContextOptionsBuilder options)
        => options.UseSqlServer("Data Source=.;Initial Catalog=ShopDB;Integrated Security=True");
}
```

#### Example: Querying Data  
```csharp
using var db = new ShopContext();

var cheapProducts = db.Products
    .Where(p => p.Price < 50)
    .OrderBy(p => p.Name)
    .ToList();

foreach (var p in cheapProducts)
    Console.WriteLine($"{p.Name} - {p.Price}");
```

### Transactions  
EF Core automatically wraps SaveChanges() calls in transactions.
You can also manage transactions manually if needed.

```csharp
using var transaction = db.Database.BeginTransaction();
try
{
    db.Products.Add(new Product { Name = "Headset", Price = 70 });
    db.SaveChanges();

    db.Products.Add(new Product { Name = "Monitor", Price = 250 });
    db.SaveChanges();

    transaction.Commit();
}
catch
{
    transaction.Rollback();
}
```

LINQ queries are executed only when enumerated (deferred execution).  
```csharp
var q = db.Products.Where(p => p.Price > 100); // not executed yet
var list = q.ToList(); // executed here
```

## Asynchronous Data Access  
Almost all EF Core and ADO.NET APIs have asynchronous versions.  
that free up threads while waiting for database operations to complete.

```csharp
var expensiveProducts = await db.Products
    .Where(p => p.Price > 200)
    .ToListAsync();
```

### Connection Strings: Where Should They Be Stored?  
For small projects or local development, it's acceptable to store your connection strings in appsettings.json.  
However, you must be careful not to commit this file to Git if it contains sensitive information.  
  
In production environments—especially when running in the cloud (Azure, AWS, Docker, Kubernetes)—storing connection strings in appsettings.json is not secure.  
Instead, the recommended approach is to store them in a secure secrets management system, such as:  

- Azure Key Vault
- Environment Variables
- Azure App Configuration

These services provide encryption, access control, secret rotation, and prevent accidental exposure of credentials.
