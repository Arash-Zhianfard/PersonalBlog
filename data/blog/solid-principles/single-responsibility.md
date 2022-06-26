---
title: Single Responsibility
date: '2021-05-02'
tags: ['Single-Responsibility','Solid-Principles-in-c#','Object-Oriented-Programming']
draft: false
summary: '
A class should have a single responsibility or should have one and only one reason to change.
'
---

## A class should have one responsibility/purpose.

**In other words a class should have one and only one reason to change**

Consider the following class.

```csharp
 public class UserService
    {
        public void Register(string email, string password)
        {
            //Implementation detail for user registration
        }
        public UserInvoice CalcInvoices(double amount)
        {
            //Implementation detail for user's invoice
        }
        public bool SendEmail(MailMessage message)
        {
            //Implementation detail for sending an email to a user
        }
    }
```

This class is responsible for **user's registration**, **returning the user's invoice** and also **sending emails to a user**.

Three completely deferent responsibilities in one class therefore any change in the functionally of one those methods require modification in the class.

## Solution

Wouldn’t be better if we chunk this class to three class with one responsibility?

```csharp
public class UserService
    {
        public void Register(string email, string password)
        {
            //Implementation detail for user registration
        }
    }
```

```csharp
public class InvoiceService
    {

        public UserInvoic Calc(double amount)
        {
            //Implementation detail for user's invoice
        }
    }

```

```csharp
public class EmailService
    {
        public bool Send(MailMessage message)
        {
            //Implementation detail for sending an email to a user
        }
    }

```

This way we have a better separation of concerns and each class have single responsibility.
