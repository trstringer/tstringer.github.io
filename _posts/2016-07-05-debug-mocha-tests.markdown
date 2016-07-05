---
layout: post
title:  "Debug Mocha Tests"
date:   2016-07-05 08:00
categories: nodejs mocha
---
This blog post is serving just as much as personal documentation for me to come back to, but here is a quick little guide on one way to debug mocha tests.

Mocha makes testing super easy with node.js, and it's a widely accepted library to handle this.  I love it, and I embrace it.  It's simple to `npm install --save-dev mocha` and then off to the races with creating your unit tests.

But much like with any executable code, it's simply a matter of time until you need to debug it.  Unit tests are no different... you'll have to debug them.

It's not a terribly straightforward operation to debug mocha tests, but here is how I do it.

First step is to install [`node-inspector`](https://www.npmjs.com/package/node-inspector) by running `npm install -g node-inspector`.

The next step is to kick it off by running `node-inspector`.  When you do this, you'll get a similar message:

```
Node Inspector v0.12.8
Visit http://127.0.0.1:8080/?port=5858 to start debugging.
```

Now you can start mocha, but the way I do it is to start it with the `--debug-brk` flag so that it starts in debugging mode and breaks immediately.  This gives you the chance to start up the tooling.

Open up Chrome and navigate to the URL that node-inspector dumped out and start debugging!  Something I do is create a separate npm script to start mocha in this manner, making it an even quicker operation to start diving into debugging my mocha tests.

Enjoy!