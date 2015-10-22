---
layout: post
title:  "Passing in Command Line Arguments while Debugging a Node.js Application in Visual Studio Code"
date:   2015-10-22 09:20
categories: vscode nodejs
---
Visual Studio Code makes it really easy (and getting easier!) to debug node.js applications. One of the things you may need to do is pass in command line arguments to your node application when debugging.

Here is some sample node.js application code...

```javascript
var cmdLineArg = process.argv[2];
 
if (cmdLineArg === undefined)
    console.log("no cmdline argument passed!");
else
    console.log("cmdline argument passed :: " + cmdLineArg);
```

If you were to use the Visual Studio Debugger without making any changes, you would see the following output...

```
no cmdline argument passed!
```

So how exactly do you pass command line arguments to node when debugging inside of Visual Studio Code? Simple! Just modify launch.json and specify the args property of your current configuration with your debug command line arguments...

```json
    // Command line arguments passed to the program.
    "args": [
        "hello!"
    ]
```

Now when you debug the node application in Visual Studio Code, you’ll see the following output...

```
cmdline argument passed :: hello!
```

Powerful, fun, and easy-to-configure debugging in VS Code!