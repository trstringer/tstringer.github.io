---
layout: post
title:  "Easily Log to Azure"
date:   2015-12-30 08:00
categories: nodejs javascript azure azure-storage 
---
There is no question about it, Node.js is a first-class citizen in Azure.  As more and more applications live in the cloud, the question of common application requirements start to arise.

Take this for instance, I'm currently writing a node.js web app in Azure, and I need to find a way to quickly and easily log in the cloud.  I couldn't find anything that fit the bill, so I created a module to easily log to Azure.  This module abstracts a large portion of the data access and "nitty gritty" of working with Azure storage to make it a quick and seamless operation.

The inner-workings of this module are that it connects to your (existing) storage account, and either creates or reuses a specified table (with defaults so that you don't need to worry about that).

This module is exactly what I need, and works for me.  Now in my web app, I can add middleware to my express layer to log my errors.

## [Azure Logger (npm)](https://www.npmjs.com/package/azure-logger)

```
npm install --save azure-logger
```

The usage is pretty simple, and there are a lot of assumptions/defaults to make the calls minimal and easy...

```javascript
var logger = require('azure-logger');

// use the default options including the default 
// table name "loggerdefault" and an entry type 
// of "information"
logger.log(myObject, function (err, res) {
    if (!err) {
        // successfully inserted object, which 
        // is returned as the res param
    }
});
```

And then to subsequently read the data...

```javascript
logger.get(function (err, entries) {
    if (!err) {
        // success 
    }
});
```

I have future plans to add CLI functionality to make reading the entries easier, so that you don't have to plug that functionality into your own application.  But for now this gets data in.

Enjoy!