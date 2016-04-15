---
layout: post
title:  "Make Visual Studio Code your Git Editor"
date:   2016-04-15 08:00
categories: social 
---
Visual Studio Code v1.0.0 was released yesterday, bringing it out of beta!  With this new release came some pretty awesome features, and one of my favorites is, without a doubt, the ability to [make VS Code your default git editor](https://code.visualstudio.com/Updates#_setup).

So what exactly does that mean for a git user?  Well that means you can now use VS Code to handle your editor needs from git for operations such as editor commit messages, rebasing, diff'ing, etc.

So how do we set this up?  Feel free to use the previously linked reference for the official documentation, but for the sake of a one-stop read for this blog post you'd set this up by doing the following for the initial setup: `git config --global core.editor "code --wait"`

What did we just do??  All we did was set the default editor to VS Code (specifically passing the `--wait` argument which is new, forcing the calling process/CLI to wait until the launched code process closes before continuing, a prerequisite for a git editor).

Now we need to set the `diff` and `difftool` configurations.  First open up the configuration with `git config --global -e` and then add the following configuration...

```
[diff]
  tool = vscode-diff
[difftool "vscode-diff"]
  cmd = code --wait --diff $LOCAL $REMOTE
```

Now when you do a `git difftool <commit> <commit>` git will open up VS Code and show the file diff (great experience!).

This also now makes editor experiences with git for things like a rebase open up in VS Code.  This is a super great advancement that further ingrains VS Code as a first-class editor!

Enjoy!