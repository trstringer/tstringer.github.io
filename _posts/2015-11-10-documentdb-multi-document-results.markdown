---
layout: post
title:  "Working with Multi Document Results from DocumentDB"
date:   2015-11-10 14:00
categories: nodejs npm npmjs documentdb
---
Oftentimes when dealing with DocumentDB you could be querying the documents for only a single document.  This a common use-case, but there are going to be times when your DocumentDB query will return multiple documents, and you'll need to consume them.

There are a few ways to go about consuming multi-document queries (in this case, I'll be using the DocumentDB Node.js SDK).

## Iterate Over the Documents

If you want to iterate over the documents with the `QueryIterator`, you can use the `forEach()` method.  This method will run a function for each element...

```javascript
// ... omitted code to pull and/or construct
// ... the collection link (collection._self)
//
var docQuery = 'SELECT * FROM questions q';
ddbClient.queryDocuments(collection._self, docQuery)
    .forEach(function (err, document) {
        if (!err) {
            if (!document) {
                // after the last document has been  
                // reached, the returned resource/doc 
                // will be undefined
                //
                console.log('no more documents!!!');
            }
            else {
                console.log('document found: ' + document.text);
            }
        }
    });
```

## Get an Array of the Documents

Conversely, if you want to grab an array of the documents, you can use the `QueryIterator` method `toArray()`...

```javascript
// ... omitted code to pull and/or construct
// ... the collection link (collection._self)
//
var docQuery = 'SELECT * FROM questions q';
ddbClient.queryDocuments(collection._self, docQuery)
    .toArray(function (err, documents) {
        if (!err) {
            console.log('found ' + documents.length + ' documents...');
            for (var i = 0; i < documents.length; i++) {
                console.log(documents[i].text);
            }
        }
    });
```

As you can see, there are a few ways to work with what you need when dealing with multi-document result sets from DocumentDB.

Enjoy!