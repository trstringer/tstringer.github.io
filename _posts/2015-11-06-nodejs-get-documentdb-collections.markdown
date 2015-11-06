---
layout: post
title:  "Get all DocumentDB Collections from Node.js"
date:   2015-11-06 09:00
categories: nodejs npm npmjs documentdb
---
Yesterday I wrote about [how to get all databases in a DocumentDB account](http://tstringer.github.io/nodejs/npm/npmjs/documentdb/2015/11/05/nodejs-get-documentdb-databases.html).  Here's a quick little snippet on how to list out all **collections** in a DocumentDB account (and correlate them with their containing database)...

```javascript
var DocumentClient = require('documentdb').DocumentClient;

var endpointUrl = '... url ...';
var masterKey = '... key ...';
var ddbClient = new DocumentClient(endpointUrl, {masterKey: masterKey});

ddbClient.queryDatabases('SELECT d.id, d._self FROM databases d')
    .forEach(function (err, database) {
        if (database) {
            console.log(database.id + ' -- ' + database._self);
            ddbClient.queryCollections(database._self, 'SELECT c.id, c._self FROM collections c')
                .forEach(function (err, collection) {
                    if (collection) {
                        console.log('  ' + collection.id + ' -- ' + collection._self);
                    }
                });
        }
    });
```

This can be handy to dump out all of the collections in your DocumentDB account.

Enjoy!