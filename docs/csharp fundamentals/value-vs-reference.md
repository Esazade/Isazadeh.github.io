---
layout: default
title: "Value vs Reference Type"
parent: "Fundamentals"
nav_order: 6
---

# Value Type vs Reference Type in C#

Sometimes you run into a bug that makes absolutely no sense.
You change one variable — and somehow, another one changes too!
That’s the exact moment you realize what Value Types and Reference Types really mean.
---

## Value Type

Imagine everyone has their own box.
When you copy what’s inside, you just get a new version — not the original one.
It’s like photocopying your friend’s notebook: writing on your copy doesn’t change theirs
---

## Real Example

```csharp
int a = 10;
int b = a;
b = 20;

Console.WriteLine(b);  // 20

```

## Reference Type

But this one’s different.
Instead of having your own box, you’re holding a note with the address of the real box written on it.

So if you give that note to someone else, they can open and change the same box you’re pointing to.
Whatever one person changes inside it — everyone else sees it too


## Real Example

```csharp
Book b1 = new Book();
b1.Title = "C# Basics";

Book b2 = b1;
b2.Title = "PHP";

Console.WriteLine(b1.Title);  // php
```
Now, if you do it this way instead

```csharp
Book b1 = new Book();
b1.Title = "C# Basics";

Book b2 = new Book();
b2.Title = "PHP";
```
This means each one is a completely separate book on its own shelf.
If you change the title of one, the other stays exactly the same