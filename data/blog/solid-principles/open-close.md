---
title: Open-Close Principle
date: '2021-05-02'
tags: ['Open-close-principle','Solid-Principles-in-c#','Object-Oriented-Programming']
draft: false
summary: '
Classes should be open for extension, but closed for modification.
'
---

## Classes should be open for extension, but closed for modification.

We have the flowing class for sending notification to users

```csharp showLineNumbers
public class NotificationService
{
    public void Notify(NotifyMessage message)
    {
        var emailService = new EmailService();
        emailService.Send(message);
    }
}
```

After some while, customer ask for the SMS notification.

Probably, you might think that by adding an extra `else if` condition, we are able to implement it.

Something like this

```csharp showLineNumbers
public class NotificationService
{
    public void Notify(NotifyMessage NotificationType type)
    {
        if (type == NotificationType.Email)
        {
            var emailService = new EmailService();
            emailService.Send(message);
        }
        else if (type == NotificationType.Sms)
        {
            var smsService = new SmsService();
            smsService.Send(message);
        }
    }
}
```

But what if they ask for the push notification?

Adding extra `else if` condition!?

Definitely not, because there is an issue with this implementation, every time a new notification type needs to be added to the system, we have to modify this class, so it is not closed for modification.

## Solution

First we create base class for all types of notifications.

```csharp showLineNumbers
public interface INotification
{
    void Notify(NotifyMessage message);
}
```

Then a separate class will be used for sending SMS notifications.

```csharp showLineNumbers
public class SmsNotification : INotification
{
    public void Notify(NotifyMessage message)
    {
        var smsService = new SmsService();
        smsService.Send(message);
    }
}
```

Same for the email notification.

```csharp showLineNumbers
public class EmailNotification : INotification
{
    public void Notify(NotifyMessage message)
    {
        var emailService = new EmailService();
        emailService.Send(message);
    }
}
```

Then simply we add push notification to system as follow.

```csharp showLineNumbers
public class PushNotification : INotification
{
    public void Notify(NotifyMessage message)
    {
        var pushService = new EmailService();
        pushService.Send(message);
    }
}
```

with this approach classes are _**open for extension but close for modification**_.
