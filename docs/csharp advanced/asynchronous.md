---
layout: default
title: "Asynchronous Programming"
parent: "CsharpAdvanced"
nav_order: 3
---

# Why Asynchronous Programming?

Modern apps do a lot of **I/O** (disk, database, web APIs) and sometimes **long-running work**.  
If you block the main thread while waiting, users see freezes, servers handle fewer requests, and battery drains faster.

**Asynchronous programming** lets your code _start_ a task (e.g., read a file, call an API), then **yield** control while the OS/Runtime finishes the work. When the result is ready, your method **resumes** right where it left off. UI stays responsive; servers scale better.

---

# Synchronous vs Asynchronous

| Aspect | Synchronous | Asynchronous |
|---|---|---|
| Execution | One step after another | Can yield and resume later |
| Main thread/UI | Blocks (freezes) during waits | Stays responsive |
| Server scalability | Fewer concurrent requests | Many more concurrent requests |
| When to use | Short CPU work | I/O waits, long tasks, concurrency |

**Synchronous**
```csharp
string text = File.ReadAllText("data.txt"); // blocks until disk I/O completes
Console.WriteLine(text);
```

**Asynchronous**
```csharp
string text = await File.ReadAllTextAsync("data.txt"); // yields while OS reads
Console.WriteLine(text);
``` 

## async/await  
- async marks a method that can await tasks and will be rewritten by the compiler into a state machine.
- await pauses the method until the awaited Task completes, then resumes.
- While paused, the current thread is free to do other things (handle UI events, process other requests).

```csharp
async Task<int> CalculateSumAsync()
{
    await Task.Delay(2000); // simulate async work (I/O-like wait)
    return 42;
}
```

### Task (for methods without a return value)
```csharp
async Task DoWorkAsync()
{
    await Task.Delay(1000);
    Console.WriteLine("Work completed!");
}
```

### Task<T> (for methods with a return value)
```csharp
async Task<int> CalculateAsync()
{
    await Task.Delay(1000);
    return 42;
}
```

## CancellationToken  
Cancellation lets you stop a running asynchronous operation before it finishes, in a cooperative and controlled way.

### Example (Downloading with cancellation)
```csharp
static async Task DownloadFileAsync(string url, string path, CancellationToken token)
{
    using HttpClient client = new HttpClient();
    using var response = await client.GetAsync(url, HttpCompletionOption.ResponseHeadersRead, token);
    using var stream = await response.Content.ReadAsStreamAsync(token);
    using var fileStream = File.Create(path);

    await stream.CopyToAsync(fileStream, 81920, token);
}
```

## Parallel vs Asynchronous  
Parallel: runs multiple tasks at the same time on multiple cores (CPU-bound).
Asynchronous: waits efficiently for I/O or external operations (I/O-bound).

### Example (Parallel CPU-bound)  
```csharp
Parallel.For(0, 10, i => DoHeavyWork(i));
```

### Example (Async I/O-bound) 
```csharp
await DownloadFileAsync("https://example.com");
```

## Combining Tasks
You can run multiple tasks concurrently using Task.WhenAll() or Task.WhenAny().

```csharp
var task1 = DownloadFileAsync("file1");
var task2 = DownloadFileAsync("file2");

await Task.WhenAll(task1, task2);
Console.WriteLine("Both files downloaded");
```
- Task.WhenAll() runs all tasks concurrently and waits until all of them are completed.
- Task.WhenAny() waits until any one of the tasks has completed.

## Common Pitfalls & Best Practices

### Avoid async void
```csharp
// Bad - hard to handle exceptions
async void ButtonClick() { }

// Good
async Task ButtonClickAsync() { }
```

### Don't block async code
```csharp
// Bad - causes deadlocks
var result = GetDataAsync().Result;

// Good
var result = await GetDataAsync();
```

## Exception Handling in Async Code
```csharp
async Task ProcessWithRetryAsync()
{
    try
    {
        await ProcessDataAsync();
    }
    catch (HttpRequestException ex) when (ex.Message.Contains("timeout"))
    {
        // Retry logic
        await Task.Delay(1000);
        await ProcessDataAsync();
    }
}
```

