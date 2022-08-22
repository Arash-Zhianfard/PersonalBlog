---
title: Naming Tips
date: "2022-08-19"
tags:
  ["Naming-Tips", "Naming-Tips-in-c#", "Naming-Tips-C#10", "Naming-Tips-C#9"]
draft: false
summary: "In general finding good a name for variables or any other entities is difficult."
---

In general finding good a name for variables or any other entities is difficult.

This article focus on naming tips and conventions and common naming mistakes which developers make.

**1-Follow PascalCasing to name a `class`, `struct` ,`record` or public member(`fields, properties, events, methods, and local functions`).**

Few Examples

- Classe :

```csharp {1} showLineNumbers
public class User { }
```

- Method :

```csharp {3} showLineNumbers
public class UserService
{
    public void Get(int id)
    {
    }
}
```

---

**2-For interfaces, use pascal casing in addition to prefixing the name with an `I`**

```csharp {1} showLineNumbers
public interface IExample
{
}
```

---

**3-Use camel casing in addition to prefixing the name with an `_`**

```csharp {3} showLineNumbers
public class Example
{
   private bool _privateFiled;
}
```

---

**4-Use the s\_ prefix for private or internal static fields**

```csharp {3} showLineNumbers
public class Example
{
   private static bool s_privateStaticFiled;
}
```

---

**5-Use the t\_ prefix for private or internal thread static.**

```csharp {4} showLineNumbers
public class Example
{
   [ThreadStatic]
   private static bool t_privateThreadStaticFiled;
}
```

---

**6-Use Boolean variables with `is`, `has`, `can` and `should` prefixed**

```csharp {3} showLineNumbers
internal class Example
{
    private bool _hasFinished = false;
}
```

---

## Common Mistakes

**1-Repeating class's name in method's name**

Consider changing following code

```csharp showLineNumbers
internal class CourseService
{
    public List<Course> GetAllCourses()
    {
        //implementation detail
    }
}
```

To

```csharp showLineNumbers
internal class CourseService
{
    public List<Course> GetAll()
    {
        //implementation detail
    }
}
```

**Reason:**

There is no need to mention `Course` as a part of the method's since it is calling from `CourseService`.

**2-Use method overloading instead of long name**

Consider changing following code

```csharp showLineNumbers
internal class CourseService
 {
    public Course GetCourseById()
    {
        //implementation detail
    }
    public Course GetCourseByName()
    {
        //implementation detail
    }
 }
```

To

```csharp showLineNumbers
internal class CourseService
{
    public Course GetCourse(int id)
    {
        //implementation detail
    }
    public Course GetCourse(string name)
    {
        //implementation detail
    }
}
```

**Reason:**

What we are try to achieve is to getting a course based on different filters ,using method overloading is better than using long descriptive names.
