---
layout: post
title:  "Manage Deployments with an Azure Web App"
date:   2015-11-30 08:00
categories: nodejs azure 
---
When working with continuous deployment with an Azure web app, it is extremely helpful to be able to list out and even rollback a deployment to a previous deployment in the not-so-unlikely situation where you will simply need to revert to a previous commit.

I am a huge proponent of the Azure cross-platform CLI, and I believe that becoming fluent with this tool will allow you to quickly and easily manage your Azure resources.  This blog post will reference the commands to work with an Azure web app's deployments through the use of the [azure x-plat CLI](https://www.npmjs.com/package/azure).

## List your current deployments

```
azure site deployment list your-web-app
```

*`your-web-app` is the placeholder for you web app's name*

In my test web app, the resulting deployments appear like this...

```
Time                          Commit id   Status   Author           Message
----------------------------  ----------  -------  ---------------  -------------------------
2015-11-30T14:28:27.3754476Z  8f7f265171  Active   Thomas Stringer  Changed world to universe
2015-11-30T14:27:20.6637589Z  54a507921a  Success  Thomas Stringer  Added hello world
2015-11-25T15:36:24.9567456Z  15f19518da  Success  Thomas Stringer  Initial commit
```

In my case, same I want to rollback my web app to commit `54a507921a` where my web app displays `Hello, World!` instead of `Hello, Universe!`.

## Redeploy/rollback a previous deployment commit

In order to rollback to a previous commit, simply run the following command...

```
azure site deployment redeploy <commitId> <webAppName>
```

For me, this command translates to...

```
azure site deployment redeploy 54a507921a web-app-test1
```

Once this command completes, the current deployments are re-listed again, now showing that my previous commit is now the desired deployment...

```
Time                          Commit id   Status   Author           Message
----------------------------  ----------  -------  ---------------  -------------------------
2015-11-30T14:28:27.3754476Z  8f7f265171  Success  Thomas Stringer  Changed world to universe
2015-11-30T14:37:11.3060446Z  54a507921a  Active   Thomas Stringer  Added hello world
2015-11-25T15:36:24.9567456Z  15f19518da  Success  Thomas Stringer  Initial commit
```

Simple as that!  Quickly redeploy/rollback to a previous deployment commit with the Azure x-plat CLI.

Enjoy!