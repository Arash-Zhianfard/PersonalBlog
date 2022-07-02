---
title: Dependency Inversion Principle
date: '2022-06-28'
tags: ['Dependency-Inversion','Solid-Principles-in-c#','Object-Oriented-Programming']
draft: false
summary: '
High-level modules should not depend on low-level modules. Both should depend on abstractions.
'
---

## High-level modules should not depend on low-level modules. Both should depend on abstractions.

The definition could be a little difficult to understand, but let's see what it means by an example.

The following repository class is responsible for fetching all users from database.

```csharp showLineNumbers
public class UserRepository
{
    private readonly string _connectionString;

    public UserRepository(string connectionString)
    {
        _connectionString = connectionString;
    }

    public List<User> GetAll()
    {
        using var con = new SqlConnection(_connectionString);
        con.Open();
        var users = con.Query<User>("select * from users").ToList();
        return users;
    }
}
```

As you my noticed `connection string` is passing as parameter to this class.

The below `UserService` class consuming the `UserRepository` to get users' info from database.

```csharp showLineNumbers
public class UserService
{
    public List<User> GetAll()
    {
        var cs = "Data Source=localhost;Initial Catalog=Test;User ID=UserName;Password=Password";
        var userRepository = new UserRepository(connectionString: cs);
        var users=userRepository.GetAll();
        return users;
    }
}
```

But there is an issue with above code ,any class that need to get the data from the userRepository must pass connectionString as parameter.

**`UserService` class shouldn't know anything about the `UserRepository` implementation detail.**

## Solution

First create a interface for the repository.

```csharp showLineNumbers
public interface IUserRepository
{
    IEnumerable<User> GetAll();
}
```

The blew code is same as the code we had, the only difference is it gets connection string from `appSetting`.

```csharp showLineNumbers
public class UserRepository : IUserRepository
{
    private readonly string _connectionString;

    public UserRepository(IOptions<DbSetting> dbSetting)
    {
        _connectionString = dbSetting.Value.ConnectionString;
    }

    public List<User> GetAll()
    {
        using var con = new SqlConnection(_connectionString);
        con.Open();
        var users = con.Query<User>("select * from users").ToList();
        return users;
    }
}
```

In the Blow code, `UserService` is depended upon abstraction(in this case `IUserRepository`) rather than concrete class(`UserRepository`).

In this implementation, all thing that UserService knows is that there is an interface or a contract that it's able to get users from database.

```csharp showLineNumbers
public class UserService
{
    private readonly IUserRepository _userRepository;
    public UserService(IUserRepository userRepository)
    {
        _userRepository = userRepository;
    }
    public List<User> GetAll()
    {
        var users = _userRepository.GetAll();
        return users;
    }
}
```

![Dependency-Inversion](https://i.ibb.co/MZJbB1G/66.jpg)
