---
layout: post
title:  "Incrementing the Version of your npm Package"
date:   2015-10-29 12:00
categories: npm npmjs
---
When developing a package and using npm to package and distribute it, one of the more obvious features of it is the use of the `version` key in `package.json`.  When patching or building on the module it might be a common reaction to just modify the `package.json` file directly to change the version, but npm provides a handy mechanism to increment these numbers.

Simply use `npm version major|minor|patch` to increment the appropriate part of the version.

Now for a quick little example, I've created a sample package locally.

```
npm list
```

I see the output showing we are working with a version `1.0.0`.

```
npm-test@1.0.0 C:\nodejs\testing\npm-test
```

Now say we just patched a bug and we want to increment the patch level...

```
npm version patch
```

We see the output is the new version...

```
v1.0.1
```

Let's patch another bug and increment this patch level again...

```
npm version patch
```

As you would expect...

```
v1.0.2
```

But now let's say you add a non-breaking feature, so you want to increment your minor...

```
npm version minor
```

The new version...

```
v1.1.0
```

A few things to note here, not only did it increment the minor level, but it reset the patch level to zero (0), as per the [Semantic Versioning guidelines](http://semver.org/).

And the same behavior when you increment the major level...

```
npm version major
```

The new version...

```
v2.0.0
```

As you can see here, we have incremented the major level and set the minor level back to zero.

This is an easy mechanism to adjusting your npm package version without having to manually modify `package.json`, keeping it consistent and error-proof.


Enjoy!