---
title: General Tips/Recommendations To Improve Code Quality In C#.(part-1)
date: "2022-08-22"
tags:
  [
    "C#-improve-code-quality",
    "when-use-var-keyword-c#",
    "C#10",
    "target-typed-C#9",
    "C#-10-string-interpolated",
  ]
draft: false
summary: "General Tips/Recommendations To Improve Code Quality In C#."
---

There are many books and blogs about clean code and how to make it more efficient, but I couldn't find any comprehensive reference that helps me to improve my code and reviewing the tips and recommendations.

I will show number of cases which we are able to improve code readability and efficiency, I also mentioned new c# features which could help us to achieve them.

I must emphasize that these are recommendations, and every developer could have a different opinion about them.

**1-Use explicit type when type is not clear ,some developers tend to use `var` everywhere just because it’s convenient.**

Consider changing following code

```csharp
var file = File.CreateText("example.txt");
```

To

```csharp
StreamWriter file = File.CreateText("example.txt");
```

---

**2-Add following suffix to local variable to specify the type if you want to use `var` keyword.**

- M: infers decimal
- D: infers double
- F: infers float
- L: infers long
- UL: infers ulong

---

**Note: Use explicit typing if you want to have nullable reference types enabled, `var` keyword always implies a nullable reference type even if the expression type isn't nullable.**

---

**3-Use C# 9 `target-typed new` syntax for instantiating objects. you can specify the type first and then use `new` without repeating the type**

Consider changing following code

```csharp
var course = new Course();
```

To

```csharp
Course course = new(); //C# 9
course.CreatedOn = new(1967, 12, 26); //C# 9
```

---

**4-Use C# 6 Formatting interpolated strings instead of string.Format()**

Consider changing following code

```csharp
Console.WriteLine(string.Format("we have {0} students and  average grade is {1:n2}", studentCount, averageGrade));
```

To

```csharp
Console.WriteLine($"we have {studentCount} students and  average grade is {averageGrade:n2}");
```

---

**5-Use C# 10 string interpolated strings**

Consider changing following code

```csharp {3} showLineNumbers
string firstname = "Jack";
string lastname = "Smith";
string fullname = firstname + " " + lastname;
```

To

```csharp {3} showLineNumbers
string firstname = "Jack";
string lastname = "Smith";
string fullname = "{firstname} {lastname}";
```

---

**6-Specify the `null` to acknowledge that a `null` value could be returned.**

Consider changing following code

```csharp
string firstName = Console.ReadLine();
```

To

```csharp
string? firstName = Console.ReadLine()
```

---

**7-Use static `System.Console` in console application to not repeat the code(C# 6).**

```csharp showLineNumbers
using static System.Console;
WriteLine(string.Format("we have {0} students and  average grade is {1:n2}", studentCount, averageGrade));
WriteLine($"we have {studentCount} students and  average grade is {averageGrade:n2}");
```

---

**8-Use braces with `if` statements Although your code can be written without the curly braces, it’s highly recommended to use them since it may cause bugs in your application sometimes.**

Consider changing following code

```csharp showLineNumbers
if(condition) process();
```

To

```csharp showLineNumbers
if(condition)
{
   process();
}
```

---

**8-Consider using explicit access modifiers,even for private members.**

Consider changing following code

```csharp {3} showLineNumbers
class Example
{
    const string firstname="Jack"
}
```

To

```csharp {3} showLineNumbers
internal class Example
{
   private const string firstname="Jack"
}
```

---

**9- Consider specify the name of the parameter as well as its value, if they provide more meaning for functions' declaration.**

Consider changing following code

```csharp
Person person = new Person() { FirstName = "Jack", LastName="Smith", DateOfBirth = new DateTime(1993, 1, 1)};
```

---

**10-Consider derive an enum type if you don't need values that are big.**

Since `int` variable use by default,if we use `byte`,it can be reduced memory requirements by 75%, 1 byte per value instead
of 4 bytes.

- Derive from `byte` if there are up to 8 options.
- Derive from `ushort` if there are up to 16 options.
- Derive from `uint` if there are up to 32 options.
- Derive from `ulong` if there are up to 64 options.

```csharp showLineNumbers
public enum Exmaple : byte
{
   value1 = 1,
   value2 = 2,
   value3 = 3
}
```

---

**11-Prefer using `struct` over `class` if**

- The total bytes used by all the fields in your type is 16 bytes or less
- Your type only uses value types for the fields
- Don't want derive from a type in future

Consider changing following code

```csharp showLineNumbers
internal class Example
{
    public int Property { get; set; }
    public long Property2 { get; set; }
    public bool Property3 { get; set; }
}
```

To

```csharp showLineNumbers
internal struct Example
{
   public int  Property  { get; set; }
   public long Property2 { get; set; }
   public bool Property3 { get; set; }
}
```

---
