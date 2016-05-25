---
layout: post
title:  "Write your first .NET Core Library"
date:   2016-05-24 08:00
categories: dotnet dotnet-core 
---
There has been a recent surge in information and *all new things* .NET Core, [mostly due to the release of RC2](https://blogs.msdn.microsoft.com/dotnet/2016/05/16/announcing-net-core-rc2/).  There is a lot of great excitement surrounding .NET Core these days, and I think it is much warranted.  It is turning out to be a great tool and platform, and I can personally say that I'm enjoying .NET Core already.

One of the things I've recently been playing around with is writing a library that is meant to be consumed by .NET Core.  I love the idea of modularity and units of single-responsibility, no matter if we're talking about [npm](http://npmjs.org) in the JavaScript world, [nuget](http://nuget.org) in the .NET world, or whatever medium you use to get reusable code (usually from a *package manager*).

A couple of days ago, [this reference was added to show exactly this:  How to write libraries for .NET Core and many other things that were pertinent for the topic](http://dotnet.github.io/docs/core-concepts/libraries/libraries-with-cli.html).  When I read this I really wanted to play with creating my own libraries, as I think this is going to be a large advantage of the .NET Core ecosystem.

The ability to quickly create reusable content is also a necessary feature in the ecosystem, and after a little wrestling with code and configuration I think I have it down to a science how to create a reusable .NET Core library and packaged as a nuget package.

## Prerequisites (SDK and Tools)

I love an environment where blank machine to producitivity is quick and easy, and .NET Core is right up there.  So what do you need?  Well, you need the SDK and tools ([navigate to your platform of choice](https://www.microsoft.com/net/core#windows)).  And of course you need an editor/IDE as well.  My personal favorite for .NET Core, node.js, and other text requirements (I'm currently using it to write this blog post!) is [Visual Studio Code](http://code.visualstudio.com).  Once you have the SDK and CLI tools, as well as an editor (any will work, I just personally recommend VS Code), you should be ready to go.

## First steps...

First thing's first.  We need to create the base component for the library by running `dotnet new`.

```
$ mkdir ILoveMath
$ cd ILoveMath
$ dotnet new
```

## Library-ify it

When you run `dotnet new` it is *perfect*... for writing a console application.  What we need to do is turn this into a library instead of a console app.

 - Remove/rename `Program.cs` (could just rename it and change the contents, but seems more natural to me to just remove the file)
 - Add new source file for base class (or rename `Program.cs` appropriately)
 - Add contents to file (sample below)

```csharp
namespace ILoveMath
{
  public class DoMathThings
  {
    public int AddTwoNumbers(int num1, int num2)
    {
      return num1 + num2;
    }
  }
}
```

 - We need to change the `project.json` configuration file to reflect that we are targeting NETStandard.  We can search nuget for what version we should be using by running `nuget list netstandard -pre` for our dependency.  To target .NET Core latest, our `project.json` would look something like the following...

```json
{
  "version": "1.0.0-*",
  "dependencies": {
    "NETStandard.Library": "1.5.0-rc2-24027"
  },
  "frameworks": {
    "netstandard1.5": {}
  }
}
```

 - We can restore and build by running...

```
$ dotnet restore
$ dotnet build
```

 - And finally to package this up into a nuget package we just need to run `dotnet pack`
 - Now that we have created the `*.nupkg` file, we can now push this to a location to reference (I created a local nuget location by running `nuget sources add -name LocalPackages -source "d:\nuget"`.  I then copy my nuget package file to this location)

## Consume the library

Without a doubt, we'll want to consume this package, so now that the nuget package is added locally I can just create a .NET Core app to consume it.

```
$ mkdir MathApp
$ cd MathApp
$ dotnet new
```

I open up my new app and change the `project.json` config file to have a dependency on the new library by adding `"ILoveMath": "1.0.0"` to the dependencies section.

I change my `Program.cs` source code to reference my new library...

```csharp
using System;
using ILoveMath;

namespace ConsoleApplication
{
    public class Program
    {
        public static void Main(string[] args)
        {
            DoMathThings mathThings = new DoMathThings();
            int result = mathThings.AddTwoNumbers(1, 2);
            Console.WriteLine("Added two numbers: {0}", result);
        }
    }
}
```

And of course the expected output of running `dotnet run` on this app is `Added two numbers: 3`.

There it is!  I have created a .NET Core library and consumed it from a test app locally.

Enjoy!