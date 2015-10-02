---
layout: post
title:  "Change Last Commit"
date:   2015-10-02 18:02
categories: git
---
We all do it, and I know I speak for myself when I see that I do this *often*.  I do my day-in-day-out work with the git command line (Git Bash).  The following commands are muscle memory at this point:

```
$ git add ...
```

Followed quickly by a 

```
$ git commit -m ...
```

That commit message is something I frequently mistype.  

So now you've just committed with a commit message you immediately want to change.  How can you change this?

Let's first look at a sample git log:

```
$ git log --oneline --decorate --graph --all 
* df423b1 (HEAD -> master) 3rd commit
* fe9ba62 Second commit
* 5b83de3 First commit
```

If I want to change the last commit message from "3rd commit" to "Third commit", all I'd have to do is the following:

```
$ git commit --amend -m "Third commit"
```

And now looking back at my history I see my changed commit message:

```
$ git log --oneline --decorate --graph --all
* 7283975 (HEAD -> master) Third commit
* fe9ba62 Second commit
* 5b83de3 First commit
```

As you can see, this creates a new commit (i.e. different SHA) for the tip of the branch with the new commit message.

Simple as that!

Enjoy! 