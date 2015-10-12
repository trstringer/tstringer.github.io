---
layout: post
title:  "Search for TypeScript Definition Files"
date:   2015-10-12 08:56
categories: javascript typescript tsd vscode nodejs
---
I recently wrote about how to [*add* definition files to Visual Studio code for the use of IntelliSense](http://tstringer.github.io/nodejs/vscode/visual-studio/2015/10/07/vscode-add-nodejs-intellisense.html), but what if you simple **don't know the actual file that you need**!  The "guessing game" never works, no matter how hard you try.

So how can you search for a definition file then?  First off, you can browse to a [community-driven TSD file repository](http://definitelytyped.org/tsd/) and do a search there.  But what if you wanted to search through the command-line?

It's simple!  Just use `tsd query`.  For instance, say I'm looking to add the MongoDB type definition file to my project, but I'm not sure verbatim what it's named.  I can do a wildcard search like this:

```
tsd query mongo*
```

This comes back with the following output:


    - mongodb       / mongodb
    - mongoose-mock / mongoose-mock
    - mongoose      / mongoose


Perfect, looks like I know I want `mongodb` at this point.  What if you want to find some information about this file?  Just use the `--info` switch:

```
tsd query mongodb --info
```

This dumps out a bit of useful information (the current data returned can be seen below):


    - mongodb / mongodb
      >> MongoDB                   : github.com/mongodb/node-mongodb-native
       @ Boris Yankov              : github.com/borisyankov
       < mongodb (external module)


So there you have it!  Quick and easy searching for definition files directly through the TSD command line interface.

Enjoy!