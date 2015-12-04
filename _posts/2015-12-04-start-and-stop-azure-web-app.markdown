---
layout: post
title:  "Start and Stop an Azure Web App with the Cross-Platform CLI"
date:   2015-12-04 08:00
categories: nodejs azure 
---
There is no doubt about it that I'm a huge fan of the [azure x-plat CLI](https://www.npmjs.com/package/azure), and I will always default to the command line options when managing my Azure Web Apps (and web services in general).

If you need to start and/or stop your Azure Web App, there is no need to manually pop open the browser and navigate to the management portal.  A few simple commands and you can have this done.

## List the current status of your web app

You would probably first want to verify that the Azure Web App is in a state that you are currently expecting...

```
azure site list your-web-app-name
```

This will dump out the general information for the site, including a `Status` field which will tell you whether or not your web app is `Stopped` or `Running`.

## Stop your Azure Web App

In order to stop the web app, just run the following from the x-plat CLI...

```
azure site stop your-web-app-name
```

You'll see messages indicating that `Site your-web-app-name has been stopped`.  Probably a good idea to verify with another call to `azure site list your-web-app-name`.

## Start your Azure Web App

To start the web app into a `Running` state, run the following...

```
azure site start your-web-app-name
```

Again you'll be confronted with an info message that `Site your-web-app-name has been started`.

Better living through the CLI!

Enjoy!