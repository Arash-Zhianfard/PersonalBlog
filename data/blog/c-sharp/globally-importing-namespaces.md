---
title: Implicitly and globally importing namespaces
date: '2022-07-28'
tags: ['C# 10','globally-importing-namespaces-in-c#','.net 6']
draft: false
summary: '
There are two approaches to have global namespaces 
- Using global namespaces in one separate cs file like GlobalNamespaces.cs or any name you wish.
- Using implicitly globally import;any projects that target .NET 6.0 and therefore use the C# 10 compiler generate a .cs file in the obj folder to implicitly globally import some common namespaces like System.
'
---

Many times during the developing few namespaces need to be imported in almost all the classes in the project beside Namespaces like `System` and `System.Linq` are required in most .cs files.
With global namespace new feature in C# 10 we are to simplify importing namespaces therefore, there is no need to import these namespaces in projects over and over again.

There are two approaches to have global namespaces

1-Using global namespaces in one separate cs file like GlobalNamespaces.cs

Add a new class in your project like flowing class, then add any namespaces that you need to use inside project.

```csharp showLineNumbers
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Common; //this is a user-defined namespace
```

It's possible to define global namespaces anywhere in project ,but I recommend you to keep them in separate file

2-Any projects that target .NET 6.0 and therefore use the C# 10 compiler generate a.cs file in the obj folder to implicitly globally import some common namespaces like System.

Double click on project, editor will be opened then add following code.

```xml showLineNumbers
<ItemGroup>
    <Using Remove="System.Linq" />
    <Using Include="Common" />
</ItemGroup>
```

As you may notice `Remove` will exclude the namespace that are pre-defined by default by Visual Studio and `Include` will add namespace.

Rebuild the project and click on `Show All Files` on solution explorer

![GlobalNamespaces](https://i.ibb.co/mtBXTrn/2.jpg)

Then navigate to following path

`bin\Debug\net6.0\<Projectname>.GlobalUsings.g.cs`

Those changes affected this auto-generated implicit import file after building the project.

![GlobalNamespaces-1](https://i.ibb.co/R246NTX/3.jpg)
