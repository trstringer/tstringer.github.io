---
layout: post
title:  "Build .NET Core's corefx repo on Linux (Ubuntu)"
date:   2016-04-30 08:00
categories: dotnet dotnet-core linux ubuntu 
---
This past week I was *struggling* (to put it lightly) to get corefx (the .NET Core foundational libraries) on Linux.  After much testing and reworking it, I was finally able to get it going.  With very many lessons learned, and with more specific requirements and dependencies, I created a pull request to rework the Linux build docs.

So if you have been having issues building corefx on Linux, then check out the new documentation and hopefully it is as straightforward as possible (even a single `apt-get install` command for all dependencies!!!) and you should be up and running with corefx in Linux.

[The documentation can be found on the GitHub repository](https://github.com/dotnet/corefx/blob/master/Documentation/building/unix-instructions.md).

Enjoy!