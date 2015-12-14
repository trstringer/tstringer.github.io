---
layout: post
title:  "Getting Input and Displaying Output in a Visual Studio Code Extension"
date:   2015-12-14 08:00
categories: nodejs javascript vscode 
---
Visual Studio Code allows you to break the limits of what was originally possible but giving the programmer/user the ability to extend the IDE.  By writing [extensions for VS Code](https://code.visualstudio.com/docs/extensions/overview), the sky really is the limit!

When dealing with extensions, there's no doubt you may have to work with input and (especially) output.  There are a few ways to go about this.

### First thing's first...

Before we start working with these extensions, we need to load the `vscode` module to access the VS Code extensibility API...

```javascript
var vscode = require('vscode');
```

## Displaying (quick) output

### Information

```javascript
vscode.window.showInformationMessage('My information message!');
```

### Warning

```javascript
vscode.window.showWarningMessage('My warning message!');
```

### Error

```javascript
vscode.window.showErrorMessage('My error message!');
```

## Getting input

### Ad hoc input

In the case you want the user to be able to enter input into an input box, this can be accomplished with `vscode.window.showInputBox()`, which returns a promise to handle...

```javascript
vscode.window.showInputBox({prompt: 'What is your favorite fruit?'})
    .then(val => vscode.window.showInformationMessage('Your input was ' + val));
```

### Selectable input

Sometimes you might want to control the user with options.  This can be done with a call to `vscode.window.showQuickPick()`...

```javascript
vscode.window.showQuickPick(['option 1', 'option 2', 'option 3'])
    .then(val => vscode.window.showInformationMessage('You picked ' + val));
```

## Output channels

I saved this one for last, but output channels are a good way to have "running" output.  We can see output channels being currently used with the Git output, tasks output, etc.

In order to create a new output channel, we make a call to `createOutputChannel()`.  We specify a unique name in order to identify this channel...

```javascript
var myOutputChannel = vscode.window.createOutputChannel('MyChannelName');
```

Then to show the channel and display output, it's as simple as...

```javascript
myOutputChannel.show();
myOutputChannel.append('Visual Studio Code is awesome!');
```

Enjoy!