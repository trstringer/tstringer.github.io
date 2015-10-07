---
layout: post
title:  "Add Node.js IntelliSense to Visual Studio Code"
date:   2015-10-07 12:40
categories: nodejs vscode visual-studio
---
Programming without IntelliSense is like programming with partial vision.  It can make lookups painful, at best.  I'm a *huge* fan of Visual Studio Code, but there are a few steps you need to take when starting out on a Node.js application to enable IntelliSense.

###Install TypeScript Definition package manager

Even though I work with vanilla JavaScript and not TypeScript, it is through the use of TypeScript definition files that we can leverage Node.js IntelliSense.  So with that being said, if you don't already have **tsd** installed, you can do this through **npm**:

```
npm install -g tsd
```

###Install the Node.js type definition file

At this point, the next step is to install the type definition file for Node.js using **tsd**.  First you need to use the CLI to navigate to the root of your project (the folder that you are working with in Visual Studio Code), and then use **tsd** to install this definition file:

```
tsd install node
```

TSD will create the folder structure `\typings\node\` and dump the `node.d.ts` file there.  Once this is complete, you now have Node.js IntelliSense in Visual Studio Code!

###Additionally... (Express.js)

You may also be working with the express js framework in your Node.js web application.  I'm also a huge fan of express, and often times I follow up with installing the express type definition:

```
tsd install express
```

This will create the folder structure `\typings\express` and dump the `express.d.ts` file there.


Enjoy!