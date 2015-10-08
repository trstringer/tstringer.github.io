---
layout: post
title:  "Combine the Last Two Commits in Git"
date:   2015-10-08 09:08
categories: git
---
We all do it... we commit some code, and then realize that we need to make additional changes for the logic in that past commit.  Whether that's a typo, adding comments, or just simply appending additional related changes, what we'll end up with is **two commits** that really should just be **one commit**.  I'm not a *huge* proponent of recklessly changing git history, but in this case it would make sense.

Let's say you have the following commit history, with the past two commits that you want to be combined into a single commit:

	$ git log --oneline --decorate --graph --all
	* d0de9a7 (HEAD -> master) Made code changes related to last commit... these should be merged
	* f63c0cf Made code changes
	* 254559b Initial commit

As per the commit comments, those last two commits we want to merge together.  They should really be one commit.  The first thing to do is kick off an interactive rebase on HEAD~2:

```
$ git rebase --interactive HEAD~2
```

That will open up the editor with some interesting text:

	pick f63c0cf Made code changes
	pick d0de9a7 Made code changes related to last commit... these should be merged
	
	# Rebase 254559b..d0de9a7 onto 254559b (2 command(s))
	#
	# Commands:
	# p, pick = use commit
	# r, reword = use commit, but edit the commit message
	# e, edit = use commit, but stop for amending
	# s, squash = use commit, but meld into previous commit
	# f, fixup = like "squash", but discard this commit's log message
	# x, exec = run command (the rest of the line) using shell
	#
	# These lines can be re-ordered; they are executed from top to bottom.
	#
	# If you remove a line here THAT COMMIT WILL BE LOST.
	#
	# However, if you remove everything, the rebase will be aborted.
	#
	# Note that empty commits are commented out

So now we want to two things here:

1. keep one commit
2. squash another one

So all we need to do here is to say that we want to squash the second commit and keep (`pick`, already selected by default) the other.  Modify the editor text to read the following:

	pick f63c0cf Made code changes
	squash d0de9a7 Made code changes related to last commit... these should be merged

Save and exit the editor.

Now the editor will pop open again, and this will be for us to change the commit message for the resulting commit.  Make this whatever you think is accurate for the squashed commit:

    My squashed commit message...

Now looking at our new history, we see that those two commits became one!

	$ git log --oneline --decorate --graph --all
	* aa13048 (HEAD -> master) My squashed commit message...
	* 254559b Initial commit

Enjoy!
