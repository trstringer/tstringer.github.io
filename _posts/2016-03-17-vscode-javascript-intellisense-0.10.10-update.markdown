---
layout: post
title:  "VS Code JavaScript Module Resolution IntelliSense Status Update"
date:   2016-03-17 08:00
categories: vscode 
---
Last week I wrote a [blog post upon the release of 0.10.10 indicating that IntelliSense in this version of VS Code was "broken"](http://tstringer.github.io/vscode/2016/03/10/vscode-intellisense-breaks-0.10.10.html).  After discussion with the team ([publically on the GitHub repo](https://github.com/Microsoft/vscode/issues/3936#issuecomment-196518977)) it appears as though this is by design with the switch to Salsa.

In short, going forward with Node.js software projects developed in VS Code, create the `jsconfig.json` file in the root with the following file contents...

```json
{
  "compilerOptions": {
    "module": "commonjs"
  }
}
```

Enjoy!