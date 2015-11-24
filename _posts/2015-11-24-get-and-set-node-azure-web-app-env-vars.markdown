---
layout: post
title:  "Manage Environment Variables in a Node.js Azure Web App"
date:   2015-11-24 08:00
categories: nodejs azure 
---
Environment variables are typically a rather integral part of a node application.  When working with an Azure web app, though, it might not be extremely straightforward on where and how to manage these.

## The GUI (Azure portal)

The environment variables can be found (and modified) by navigating to your web app in the Azure portal.  Then click on **All settings**, and navigate to **Application settings**.  Scroll down to **App settings**, and these are the effective environment variables for a Node.js web app.

## Command line/script (Azure x-plat CLI)

There is an extremely handy [npm package for Azure](https://www.npmjs.com/package/azure) that fulfills the CLI/script/code desire for Azure management.  This CLI can also be used for managing the environment variables in your node web app in Azure.

### Install the azure package

```
npm install --global azure
```

### (Initial use) login

Before you start interacting with Azure with this package, you'll need to first login.

```
azure login
```

### List your node app's environment variables

```
azure site appsetting list your-web-app-name
```

*Substitute `your-web-app-name` with your Azure web app name*

### Add an environment variable to your node app

```
azure site appsetting add NEW_ENVIRONMENT_VAR=yourValue your-web-app-name
```

In this case, the new environment variable I want to add is `NEW_ENVIRONMENT_VAR` with a value of `yourValue`.

Simple as that!  A quick a powerful way to manage your environment variables in your Azure node web app.

Enjoy!