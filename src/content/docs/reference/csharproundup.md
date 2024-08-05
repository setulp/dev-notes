---
title: C# Roundup
---


## Databases

There are three main different type sof databases. Each is explained below.

- Relational
    - Relational databases are those that are good at EITHER reading or writing. They consist of rows and columns in tables (relations). Think SQL, Postgres, etc.
- NoSQL
    - Object based. No schema, can store a heirarchical data. There are not relations. Think MongoDB.
- Key-value
    - Stores data based on keys and values, like JSON or dictionaries. Think Redis.


## Garbage collections, ref/value types

C# has built in garbage collection which automatically frees up memory. This can be good but you should be careful when coding otherwise a variable that you use might be collected at some point.

References in C are handled pretty explicitly compared to C or C++. To use a reference rather than value, use the `ref` keyword in the paramter list and the argument variable.

Creating classes is almost the same as Java or C++.

Records are value types, thus are useful or data modeling.

A delegate is an object that reprsents a method.


Use a `try` method with `out` variable to handle exceptions like Python would.
```csharp

if (int.TryParse(enteredAge, out var age))
{

    if (age >= 21)
    {
        Console.WriteLine("Have a beer!");
    }
    else
    {
        Console.WriteLine("Have a root beer");
    }
}
else
{
    Console.WriteLine("You are a moron. Ages are numbers");
}
Console.WriteLine($"Welcome {name} you are {age}");

```