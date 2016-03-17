---
layout: post
title:  "VS Code JavaScript Module Resolution IntelliSense Breaks in 0.10.10"
date:   2016-03-10 08:00
categories: vscode 
---
**NOTE: Please see this [updated post](http://tstringer.github.io/vscode/2016/03/17/vscode-javascript-intellisense-0.10.10-update.html) on further explanation regarding this change in IntelliSense for JavaScript/node.js applications in VS Code**

After having applied the most recent [Visual Studio Code build (0.10.10)](http://code.visualstudio.com/updates/) I noticed that IntelliSense in my node.js applications stopped working.

Doing some digging, I saw [this issue on the VS Code GitHub repo](https://github.com/Microsoft/vscode/issues/3936).  It appears as though the default module has inadvertently changed away from `commonjs`.  Therefore in order to get IntelliSense back you need to add a `jsconfig.json` file to the root of your project with the following contents...

```json
{
  "compilerOptions": {
    "module": "commonjs"
  }
}
```

I had to restart VS Code for this to take effect, and then IntelliSense started working again!

Enjoy!