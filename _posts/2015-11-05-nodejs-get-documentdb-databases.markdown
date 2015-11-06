---
layout: post
title:  "Get all DocumentDB Database Names from Node.js"
date:   2015-11-05 18:00
categories: nodejs npm npmjs documentdb
---
With DocumentDB, being able to retrieve the database names could be a significant operation.  The DocumentDB package can be used to retrieve the database names with little work.

First you need to install the DocumentDB npm package...

```
npm install documentdb
```

Then in your JavaScript code, you need to create a new `DocumentClient` object...

```javascript
var DocumentClient = require('documentdb').DocumentClient;

var endpointUrl = '... this is the URI that can be found in the azure portal ...';
var masterKey = '... this key can also be found in the azure portal ...';
var ddbClient = new DocumentClient(endpointUrl, {masterKey: masterKey});
```

Now we have our `DocumentClient` object created, we can make a call to `queryDatabases()` and display the database names...

```javascript
ddbClient.queryDatabases('SELECT d.id FROM databases d')
    .forEach(function (err, database) {
        if (database) {
            console.log(database.id);
        }
    });
```

Done!  That is a list of all database names in your particular DocumentDB account.

Enjoy!

**EDIT**

Ryan CrawCour ([@ryancrawcour](https://twitter.com/ryancrawcour)), a Program Manager on the DocumentDB team, introduced me to an ever better way to pull this information.  You can simply use `readDatabases()` to get this information in a *much* easier-to-write-and-read snippet...

```javascript
ddbClient.readDatabases()
    .forEach(function (err, database) {
        if (database) {
            console.log(database.id);
        }
    });
```

Thanks, Ryan!