---
layout: post
title:  "My Favorite Variation of git-log"
date:   2015-10-27 12:00
categories: git
---
One of the most common operations in git is to look at the log, to see what commits have been made and where branches and remotes currently are, etc. etc. etc.

I am usually very against aliases, as I don't like the local nature that they tend to promote.  And a lot of commands and combinations are easy enough to remember and output.  So with my git-log command that I use 95% of the time, I choose not to alias this as it is a good exercise in memory.

My go-to git-log command is as follows...

```
$ git log --graph --decorate --all --oneline
```

This gives me great information, that looks really good, and is quite simple to consume quickly.  Usually if I only care about the most recent *x* commits, I'll tack on the recent commit limiting parameter.  For instance, if I only want to see the most recent 10 commits, I'll do the following...

```
$ git log --graph --decorate --all --oneline -10
```

This gives me a nice and concise output with great information.

![git log image](images/git-log.png)

Enjoy!