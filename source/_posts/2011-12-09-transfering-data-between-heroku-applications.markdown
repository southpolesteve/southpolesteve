---
layout: post
title: "Transferring Data Between Heroku Applications"
date: 2011-12-09 11:32
comments: true
categories: 
---

Today I found myself needing to move data between two heroku apps.  If you have the pgbackups addon installed, it turns out this is really easy:

```
heroku pgbackups:restore DATABASE `heroku pgbackups:url --app myapp` --app myapp-staging
```

Heroku covers the process more in depth in their [documentation]("http://devcenter.heroku.com/articles/pgbackups")

Heroku rocks!