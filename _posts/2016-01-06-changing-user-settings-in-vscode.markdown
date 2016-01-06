---
layout: post
title:  "Modify User Settings in Visual Studio Code"
date:   2016-01-06 08:00
categories: vscode 
---
Yesterday I did a [poll on twitter for how many spaces people prefer](https://twitter.com/tr_stringer/status/684488544992292865) with their JavaScript development environment editor.  It was a great response, with many (more than I thought) preferring 2 spaces instead of the default 4 spaces.

Visual Studio Code is a great environment to work in, and likewise it is *extremely* customizable.  So say you want to change the tab size from 4 to 2 and persist this in VS Code...

There are a couple of ways to navigate to the user settings configuration...

1. Through the menu bar (*File -> Preferences -> User Settings*)
2. (my favorite) The command palette (`>Preferences: Open User Settings` or type part of the string to find the option)
 
Do either of the above operations, you'll be confronted with two editor windows: **Default Settings** and **settings.json**.  The **settings.json** file is where you'll want to make the modifications/additions to your specific user settings.  What I love about the quickness in this is that you can use the **Default Settings** window as an easy reference point.

In my case, I want to change the tab size, so I see in the **Default Settings** that there is a default option set already: `"editor.tabSize": 4`.  To change this to 2, you wouldn't modify the **Default Settings**, but you would add this change to overlay in **settings.json**, by simple typing `"editor.tabSize": 2`.

Done!  Now you have customized your VS Code experience by putting your non-default settings in **settings.json**.

Enjoy!