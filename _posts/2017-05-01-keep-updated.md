---
layout: post
title: Keep updated
description: "How to keep your RHEL/CentOS system up to date"
modified: 2017-05-01
tags: [ linux, yum, centos, redhat, rhel ]
---

I've wondered a few times how best to keep a running Linux system up to date. 
Whether it's scheduling in dedicated maintenance periods and having separate staging platforms just for updates, 
or just trusting that Redhat/CentOS's packages are actually tested pretty well.

Personally I've never had a problem with them. 

Anyway this post is about one approach I've found which works well on Yum-based systems. 
I'm going to be using CentOS 7.1 for this post. 

Yum-cron is a set of scripts you can install.. via Yum, and configure quickly to run as 
a scheduled task which can download, notify, and optionally apply package updates for you.

You choose an appropriate level of updates you want and whether to apply them, and then it
just runs on the frequency you choose and does what you tell it. 

Let's get it installed.

Firstly let's install the scripts:

```bash
yum install yum-cron
```

Next, cd to the config directory
```bash
cd /etc/yum
```

Open the config with your favourite editor (I'm going to use nano)
```bash
sudo nano ./yum-cron.conf
```
At this point the config is pretty straight forward. You choose a level of updates, 
whether you want to be notified, the updates downloaded, and optionally applied. You then set
your email address at the bottom and the address you want the notifications to come from, and we're pretty much done as far as basic configuration is concerned. 

You can of course delve into this a bit more and set things such as an optional mailserver instead 
of using the local MTA, and so on. 

Next we need to enable the service to start on boot, and start it. 
I'm going to pretend I always use this method and use systemctl instead of the old RH6.x scripts ;)

```bash
systemctl enable yum-cron
systemctl start yum-cron
```

And that's it pretty much. You should get emails when updates are available, and they will be
downloaded and installed optionally. You can verify this by checking */var/log/yum.log*.

I've had this running on a few servers for a while now, for Apache and so on. You can set optional 
excludes in */etc/yum.conf* but I haven't felt the need to exclude much except MySQL.

It depends on the RPM script itself which runs when the package is installed, whether or not
the service is restarted, and is running with the latest patched binaries and libraries. 

See, there's no point installing updates if you're not restarting services to pick these patched
binaries up and use them!

Services seem to run in memory pretty well though, despite being updated on the fly. 


Oh, and there is an ansible template for yum-cron.conf [here](https://github.com/kernow5000/ansible/blob/master/templates/yum-cron.conf.j2) if you fancy using it. 
It could do with more of the options being mapped out, definitely. 


