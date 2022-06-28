---
title: Liskov Substitution Principle
date: '2022-06-28'
tags: ['Liskov-Substitution','Solid-Principles-in-c#','Object-Oriented-Programming']
draft: false
summary: '
The Liskov Substitution Principle states that any subclass object should be substitutable for the superclass object from which it is derived.
'
---

## The Liskov Substitution Principle states that any subclass object should be substitutable for the superclass object from which it is derived.

> What?!

In other words, it means that objects of a super class shall be replaceable with objects of its subclasses without breaking the application. That requires the objects of your subclasses to behave in the same way as the objects of your super class.

> It’s really good that you give me the scientific definition but how does it help us?

Consider the following class.

```csharp showLineNumbers
public class Bird
{
    public void Fly()
    {
        System.Console.WriteLine("flying");
    }
}
```

Let's create eagle class which inherit from the bird class (since eagle is a bird)

```csharp showLineNumbers
public class Eagle : Bird { }
```

But is it ok that the ostrich class inherit from the bird class because ostrich is a type of bird?!

!['Liskov-Substitution'](https://i.ibb.co/xCB1c8D/33.jpg)

I think you know the answer! **ostrich is not able to fly.**

```csharp {1, 1} showLineNumbers
public class Ostrich : Bird { }//<= wrong behavior,ostrich is not able to fly
```

## Solution

In order to address this issue we pull out flying functionality to a class that only is responsible for that purpose.

```csharp showLineNumbers
public class Bird
{
    //other bird's properties
}
public class FlyingBirds : Bird
{
    System.Console.WriteLine("flying");
}
```

In following code the ostrich class only inherit from the bird class without causing any issue.

```csharp showLineNumbers
public class Eagle : FlyingBirds { }

```

```csharp showLineNumbers
public class Ostrich : Bird { }
```

I think now it’s more clear to you now what that scientific definitions mean.

!['Liskov-Substitution'](https://i.ibb.co/wCpDRDw/55.jpg)
