---
layout: post
title:  "How exactly do npm global packages work? (Windows and Linux)"
date:   2016-02-26 08:00
categories: npmjs javascript nodejs 
---
[npm](https://www.npmjs.com/) is big and getting bigger.  Without a doubt it is simply ***the*** place to go for JavaScript packages.  One of the really cool things that can be published (creators) and consumed (users) is global packages.  A global package is typically going to be a standalone application that can be invoked outside of the scope of a packaged directory.  This gives us the ability to write and consume cross-platform applications (think: x-plat CLIs).  So cool, so powerful...

... until you need to troubleshoot why your global package isn't working ...

I'm a firm believer that in order to troubleshoot computery things then you need to have a basic to advanced level of understanding of how *"things work"*.  If you've ever had to troubleshoot a non-working global package from npm (whether yours that you published and are testing, or another one you've pulled down and isn't working on your machine) then you might be stuck at **troubleshooting step0** wondering where to start looking for an/the issue.

Before we begin diving what npm does with global packages on your machine, let's take a step back.

## How to install global packages...

This should be a review for most, but by *global package* I mean that you've installed a package like the following on your local machine...

```
npm install -g <packagename>
```

## Where did npm install the package???

Without a doubt, knowing the *location* where npm put the package is definitely where you should begin.  Thankfully npm has a handy command to list out where it'll put packages (local and global, but we'll just care about global here)...

```
npm root -g
```

My environments have the following output...

- Linux: `/usr/lib/node_modules`
- Windows: `C:\Users\<username>\AppData\Roaming\npm\node_modules`

## That's where the module is, but what about the bin file?

So the above is only a partial answer for the question of *location*, as it tells us where the modules will live, but when you invoke the "bin" (this is a layer of abstraction to invoke the code) you're not actually directly hitting the module.

If you want to find out what is actually being invoked you'll do the following...

- Linux (bash): `whereis <bin>`
- Windows (cmd): `where <bin>`

My output looks like this...

- Linux: `<bin>: /usr/bin/<bin>`
- Windows: `C:\Users\<username>\AppData\Roaming\npm\<bin>.cmd`

## Global package analysis (Linux)

So we have a "bin" in `/usr/bin` that is what is run when we type the bin name of our global package, but what exactly is this?  In Linux, this is simply a symbolic link to the app file in your global module.  You can see this by running `ls -l /usr/bin/<bin>`.  The output on my Linux machine is the following (some removed for brevity): `... /usr/bin/<bin> -> ../lib/node_modules/<module>/<binfile>` where `binfile` is the file linked to that'll run when you execute the bin.

Let's take a look at what the contents of this file are (you can run this against either the symlink or the direct app file): `cat /usr/bin/<bin>`.  I see the following...

```
#!/usr/bin/env node
require('./app.js');
```

Whoa, what is this?  I may have put this in my app file just to get it working, but this may be pretty odd syntax for a *JavaScript* file (especially for non-Linux programmers/users).  The second line looks normal, as it's just a call to `require()`.  As node developers we should all be familiar with that.  But what's with the first line? `#!/usr/bin/env node`???  In *nix, that is what's called a "shebang".  That basically tells Linux to run lines 2+ with the directive specified on the first line with the shebang operator (`!#`).  In this case, this is telling Linux to run the rest of the script from `/usr/bin/env node`.  That's a portable way of saying use `node` to run the rest of the file contents.  Therefore the 2nd line (`require(...)`) is run by nodejs.

> Note: Windows developers may have a functioning package on Windows, but when you run it in Linux you could be getting the following error trying to execute your global package: `: No such file or directory`.  This is most likely due to having CRLF line ending sequences in your bin/app file, which Linux will simply not like.  To verify that this is the case, do a grep on the bin file to see if you have CRLF sequences: `grep -U $'\015' <bin> | wc -l`.  If that returns a number greater than 0, then you have CRLF sequences possibly causing your issue.  Make sure you are pushing LFs to these files, while developing for xplat apps.

## Global package analysis (Windows)

For Windows, a global npm package is invoked with a point of abstraction with a batch file.  A typical batch file for an npm global package would look like the following...

```
@IF EXIST "%~dp0\node.exe" (
  "%~dp0\node.exe"  "%~dp0\node_modules\<module>\<binfile>" %*
) ELSE (
  @SETLOCAL
  @SET PATHEXT=%PATHEXT:;.JS;=;%
  node  "%~dp0\node_modules\<module>\<binfile>" %*
)
```

This looks complicated, but much like in Linux this is the way to invoke the bin/app file with the node executable.

## Summary

Global packages from npm are super great ways to get a cross-platform experience with apps, but like everything else code you'll end up having to troubleshooting it at one point in time or another.  I hope this information serves as good base knowledge for the way npm distributes these global packages for execution and gives you the first step on deeper troubleshooting.

Enjoy!