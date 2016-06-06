---
layout: post
title:  "Set PowerShell as Visual Studio Code's Integrated Terminal"
date:   2016-06-06 08:00
categories: vscode 
---
Visual Studio Code v1.2.0 was just released with a bunch of new great features!  One of the most desired ones was an integrated terminal.  In Windows, by default this is `cmd.exe`.

I personally use PowerShell for all of my CLI needs in Windows, as it has a better shell experience, plus easier to use coming from bash.  So I wanted to change the integrated terminal from cmd to PowerShell.

To do this, open up your user settings and add the following to your settings configuration...

```json
"terminal.integrated.shell.windows": "\\windows\\system32\\WindowsPowerShell\\v1.0\\powershell.exe"
```

Open up the integrated terminal and there it is!  PowerShell is now my integrated terminal in VS Code.

![git log image]({{ site.url }}/assets/vscode-powershell-terminal.png)

Enjoy!