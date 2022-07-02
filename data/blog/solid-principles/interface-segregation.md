---
title: Single Responsibility Principle
date: '2022-06-29'
tags: ['interface-segregation','Solid-Principles-in-c#','Object-Oriented-Programming']
draft: false
summary: '
Clients should not be forced to depend upon interfaces that they do not use.
'
---

## Clients should not be forced to depend upon interfaces that they do not use.

You may have already face this issue in your code when you needed to implement some of functionality from an interface but you forced implement all of them.this principle is address this issue.

Consider the following class.

```csharp showLineNumbers
public interface ICar
{
    void Accelerate();
    void Break();
    void SwitchToSelfDriving();
}
```

Tesla implement `ICar` since Tesla is a type of car,so far so good.

```csharp showLineNumbers
public class Tesla : ICar
{
    public void Accelerate()
    {
        //Implementation detail
    }

    public void Break()
    {
        //Implementation detail
    }

    public void SwitchToSelfDriving()
    {
       //Implementation detail
    }
}
```

But how about Golf? does Golf has `SwitchToSelfDriving` method?!

As you see in blow code we forced to implement it.

```csharp showLineNumbers
public class Golf : ICar
{
    public void Accelerate()
    {
       //Implementation detail
    }

    public void Break()
    {
       //Implementation detail
    }

    public void SwitchToSelfDriving()
    {
        //<= Golf doesn't have this feature
    }
}
```

## Solution

First we split the ICar to other interfaced with less functionality

```csharp showLineNumbers
public interface ICar
{
    void Accelerate();
    void Break();
}
```

```csharp showLineNumbers
public interface ISelfDrivable
{
   void SwitchToSelfDriving();
}
```

Wouldn’t be better if we chunk this class to three classes with one responsibility?

```csharp showLineNumbers
public class Tesla : ICar, ISelfDrivable
{
    public void Accelerate()
    {
        //Implementation detail
    }

    public void Break()
    {
        //Implementation detail
    }

    public void SwitchToSelfDriving()
    {
        //Implementation detail
    }
}
```

```csharp showLineNumbers
public class Golf : ICar
{
    public void Accelerate()
    {
          //Implementation detail
    }

    public void Break()
    {
           //Implementation detail
    }
}
```

```csharp showLineNumbers
public class EmailService
{
    public bool Send(MailMessage message)
    {
        //Implementation detail for sending an emailto a user
    }
}
```

![Single-Responsibility](https://i.ibb.co/rQdhfh7/77.jpg)
