---
layout: post
title:  "Run a Pre-Launch Task in Visual Studio Code"
date:   2015-10-14 18:00
categories: javascript vscode nodejs gulpjs
---
With the release of [Visual Studio Code v0.9.1](https://code.visualstudio.com/updates), you can now [run a task prior to launching](https://code.visualstudio.com/updates#_debugging-prelaunch-task) your application.  This is extremely helpful if when debugging you need to run some sort of task before your application kicks off.  So how exactly do you do this?  I'm working with Node.js, and I'm using gulp.js build system/task runner to work with my tasks that I want to run.

##Install gulp

We first need to install gulp globally.

```
npm install --global gulp
```

##Install gulp in your dependencies

If you already haven't created the `project.json` file, first do a quick `npm init` in the directory that your project is located in.  That'll generate our needed `project.json` file.

Then you can simple run the following in the project root to add gulp to your dev dependencies.

```
npm install --save-dev gulp
```

##Create your gulpfile.js

I created a very simple gulp file that has a single task, which kicks off another node process to run a node script.

```javascript
var gulp = require('gulp');
var exec = require('child_process').exec;

gulp.task('run-job', function (callback) {
    exec('node job.js', function (err, stdout, stderr) {
        console.log(stdout);
        console.log(stderr);
        callback(err);
    });
});
```

All this task does is kicks off the following command: `node job.js`, and I created a `job.js` file in the project root which contains the following code.

```javascript
console.log('job running...');
```

Worthless code, but it'll show us that Visual Studio Code is indeed running our gulp task.

##Set the preLaunchTask

Now we need to modify our `launch.json` file, and add a key and value to our desired debug configuration.  In the configuration that you want this pre-launch task to run, add the following key and value.

```json
"preLaunchTask": "run-job"
```

##Test it out

Now when you run the node application from Visual Studio Code (of course specifying the configuration that you added the `preLaunchTask` to), you should see the `Output` window pop up and give you the task output, indicating that it is successfully running and completed.

```
[17:57:08] Using gulpfile c:\nodejs\testing\gulptest\gulpfile.js
[17:57:08] Starting 'run-job'...
job running...
[17:57:08] Finished 'run-job' after 234 ms
```

This output shows us that gulp is indeed running the `run-job` task from the `gulpfile.js`.

Very cool and powerful stuff, this could allow us to use gulp (or any other task/build system supported) to run any tasks that we need to prior to debugging!

Enjoy! 