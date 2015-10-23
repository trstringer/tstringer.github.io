---
layout: post
title:  "Get the Latest Version of an npm Package"
date:   2015-10-23 12:00
categories: npm node.js javascript
---
[npm](https://www.npmjs.com/) is big and getting bigger.  It is an extremely powerful package manager that makes the usage of JavaScript modules easy and delightful.

There may be times when you want to see if there is a currently higher version of a package that is available.  There are a couple of ways to do this.  You might default to just going to the website ([www.npmjs.com](www.npmjs.com)).  But the beauty of npm is that the command line interface gives us all the power to do what we need.

Take this example.  Say you want to see if there is a current update for *npm itself*.  As you may already know, you can update npm by running...

```
npm install -g npm
```

That's a bit of a brute-force check, as you'll find out after the update what the latest version is (if there is even an update available).  But what would you do if you want to just **see** if there is a newer version than what you are currently running?

Simple dump your current version...

```
npm -v
```

And then pull the info for the latest version...

```
npm view npm dist-tags.latest
```

At this point, you can see what your current package (npm in this case) version is, and what the latest published package is.

Enjoy!