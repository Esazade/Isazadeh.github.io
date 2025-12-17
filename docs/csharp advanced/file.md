---
layout: default
title: "Files"
parent: "CsharpAdvanced"
nav_order: 4
---

# Working with Files in C#  

.NET provides a rich set of APIs for reading, writing, and managing files and directories through the System.IO namespace.   
These APIs work with both text and binary data and support both synchronous and asynchronous operations.   

## Paths and Directories    
The System.IO.Path, Directory, and File classes provide static methods for common file and folder operations.  

| Purpose | Class |
|--------|-------|
| Manipulate file and directory paths | `Path` |
| Create, move, and enumerate directories | `Directory` |
| Create, copy, delete, and move files | `File` |
| Object-oriented versions of `File` and `Directory` | `FileInfo` / `DirectoryInfo` |


```csharp
using System;
using System.IO;

class Program
{
    static void Main()
    {
        string path = @"C:\Temp\TestFolder";

        // Create directory
        Directory.CreateDirectory(path);

        // Check existence
        if (Directory.Exists(path))
            Console.WriteLine("Folder exists!");

        // List files
        foreach (var file in Directory.GetFiles(@"C:\Temp"))
            Console.WriteLine(file);

        // Delete directory
        Directory.Delete(path, recursive: true);
    }
}
```

### Example: Using Path Class  
```csharp
string full = @"C:\data\report.txt";
Console.WriteLine(Path.GetDirectoryName(full)); // C:\data
Console.WriteLine(Path.GetFileName(full));      // report.txt
Console.WriteLine(Path.GetExtension(full));     // .txt
```

## Reading and Writing Text Files
For text-based data, the simplest approach is using static methods in the File class or higher-level types like StreamReader and StreamWriter.  

### 1. Quick Methods: File.ReadAllText() / WriteAllText()
```csharp
string path = "data.txt";

// Write text to a file
File.WriteAllText(path, "Hello, world!");

// Read text back
string content = File.ReadAllText(path);
Console.WriteLine(content);
```

### 2. Reading/Writing Lines: File.ReadAllLines() / WriteAllLines()
```csharp
string[] lines = { "First line", "Second line" };
File.WriteAllLines("log.txt", lines);

foreach (var line in File.ReadAllLines("log.txt"))
    Console.WriteLine(line);
```

### 3. StreamReader and StreamWriter   
StreamReader and StreamWriter are for reading or writing text streams efficiently, especially large files.   

```csharp
using (StreamWriter writer = new StreamWriter("notes.txt"))
{
    writer.WriteLine("Line 1");
    writer.WriteLine("Line 2");
}

using (StreamReader reader = new StreamReader("notes.txt"))
{
    string line;
    while ((line = reader.ReadLine()) != null)
        Console.WriteLine(line);
}
```

## Reading and Writing Binary Files
For binary data (e.g., images, executables), use FileStream, BinaryReader, and BinaryWriter.   

```csharp
byte[] data = { 1, 2, 3, 4, 5 };

using (FileStream fs = new FileStream("data.bin", FileMode.Create))
{
    fs.Write(data, 0, data.Length);
}
```

```csharp
using (BinaryWriter bw = new BinaryWriter(File.Open("info.bin", FileMode.Create)))
{
    bw.Write(42);
    bw.Write("Hello");
    bw.Write(true);
}

using (BinaryReader br = new BinaryReader(File.Open("info.bin", FileMode.Open)))
{
    int number = br.ReadInt32();
    string text = br.ReadString();
    bool flag = br.ReadBoolean();
    Console.WriteLine($"{number}, {text}, {flag}");
}
```

##  Asynchronous File I/O  
Asynchronous file operations prevent blocking the calling thread during long read/write operations.   

```csharp
using var fs = new FileStream("data.txt", FileMode.OpenOrCreate, FileAccess.ReadWrite,
    FileShare.None, bufferSize: 4096, useAsync: true);

byte[] buffer = Encoding.UTF8.GetBytes("Async I/O demo");
await fs.WriteAsync(buffer, 0, buffer.Length);
```

## File and Directory Info Classes   
FileInfo and DirectoryInfo provide object-oriented wrappers around file system entities.   

```csharp
var file = new FileInfo("notes.txt");
Console.WriteLine(file.FullName);
Console.WriteLine(file.Length);
Console.WriteLine(file.LastWriteTime);

var dir = new DirectoryInfo(@"C:\Temp");
foreach (var f in dir.GetFiles("*.txt"))
    Console.WriteLine(f.Name);
```

## File Attributes and Permissions   
The FileAttributes enumeration lets you query or modify file attributes (e.g., ReadOnly, Hidden).   

```csharp
File.SetAttributes("data.txt", FileAttributes.ReadOnly | FileAttributes.Hidden);

var attr = File.GetAttributes("data.txt");
Console.WriteLine(attr);
```

## File and Stream Encoding   
For text operations, encoding determines how characters are represented as bytes.   
```csharp
using (StreamWriter writer = new StreamWriter("utf8.txt", false, Encoding.UTF8))
{
    writer.WriteLine("hi world!");
}
```

## Temporary Files and Paths   
The Path.GetTempFileName() and Path.GetTempPath() methods simplify working with temporary files.   

```csharp
string tempFile = Path.GetTempFileName();
File.WriteAllText(tempFile, "Temporary data");
Console.WriteLine($"Created: {tempFile}");
```

## Serialization (Optional but Related)   
Serialization converts an object into a stream of bytes for saving or transferring, and deserialization restores it.   

```csharp
using System.Text.Json;

var product = new { Name = "Laptop", Price = 1200 };
string json = JsonSerializer.Serialize(product);
File.WriteAllText("product.json", json);

// Read it back
var text = File.ReadAllText("product.json");
Console.WriteLine(text);
```
