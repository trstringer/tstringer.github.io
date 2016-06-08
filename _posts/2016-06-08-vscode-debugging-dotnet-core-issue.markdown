---
layout: post
title:  "Issue Debugging .NET Core Application in Visual Studio Code"
date:   2016-06-08 08:00
categories: vscode dotnet dotnet-core
---
Two of the many things that I enjoy are [Visual Studio Code](https://code.visualstudio.com) and [.NET Core](http://dotnet.github.io/).  Recently I've been using VS Code to develop my .NET Core apps, and I've been running into a funny issue.  Basically when I would create a .NET Core app and run it (or try to debug it) I would get the following error...

> WARNING: Could not load symbols for 'core-test-03.dll'. 'd:\development\dotnet\core\core-test-03\bin\Debug\netcoreapp1.0\core-test-03.pdb' is a Windows PDB. These are not supported by the cross-platform .NET Core debugger.

> Hello World!

> The program 'd:\development\dotnet\core\core-test-03\bin\Debug\netcoreapp1.0\core-test-03.dll' has exited with code 0 (0x00000000).

This is a plain .NET Core app that was created with `dotnet new` and then F5'd in Visual Studio Code.

Likewise, if I set a breakpoint in the source, it isn't hit.  Which is a larger problem when trying to debug your app.

```csharp
using System;

namespace ConsoleApplication
{
    public class Program
    {
        public static void Main(string[] args)
        {
            Console.WriteLine("Hello World!"); // set breakpoint here, won't be hit
        }
    }
}
```

The *good* news is that this is a very easy fix.  All you have to do is navigate to `project.json` and add the `"debugType": "portable"` to `buildOptions`.  Once I added that single configuration option I no longer received this warning when debugging my .NET Core app in Visual Studio Code.

Enjoy!