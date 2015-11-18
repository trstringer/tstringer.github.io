---
layout: post
title:  "Gulp Test Task with Mocha and Visual Studio Code"
date:   2015-11-18 08:00
categories: nodejs npm npmjs gulp mocha vscode
---
Being able to quickly define and run tests in your Visual Studio Code node project is one of those things that'll not only make the development process easier and more delightful, but also quicker and more efficient.  Luckily Visual Studio Code makes this possible to set up a test task (I'll be using [gulp](http://gulpjs.com/) for my build system and [mocha](http://mochajs.org/) for my test framework).

## Install mocha

```
npm install --global mocha
```

## Create tests

### Create the `test` directory and the `mytest.js` file

```powershell
mkdir test
ni test\mytest.js # powershell cmd to create file
```

### Add test code to `mytest.js`

*Note: it is a good idea to add the type definition for `mocha` by running `tsd install mocha` for IntelliSense support*

```javascript
var assert = require('assert');
var app = require('./app');

describe('My awesome test', function () {
    it('should return 1', function (done){
        assert.equal(app.returnOne(), 1);
        done();
    });
});
```

## Create gulp test task

### Install gulp

```
npm install --save-dev gulp
```

### Create `gulpfile.js`

```powershell
ni gulpfile.js # powershell cmd to create file
```

### Create gulp test task

*Note: it is a good idea to add the type definition for `gulp` by running `tsd install gulp` for IntelliSense support*

```javascript
var gulp = require('gulp');
var exec = require('child_process').exec;

gulp.task('test', function (callback) {
    exec('mocha', function (err, stdout, stderr) {
        console.log(stdout);
        console.log(stderr);
        callback(err);
    });
});
```

### Run the test task

## From the command pallete

```
task test
```

## (Best option) Shortcut keys

The default shortcut key combination for running the test task is `CTRL + SHIFT + T`.

And there you have it!!  Now once this is setup, you can simple hit the shortcut key combination and Visual Studio Code will run you mocha tests!

Enjoy!