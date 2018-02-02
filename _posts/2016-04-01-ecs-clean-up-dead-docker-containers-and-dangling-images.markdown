---
title: 'ECS: clean up dead docker containers and dangling images'
date: 2016-04-01 15:45:00 -07:00
categories:
- fixes
tags:
- aws
- ecs
- cpu
- dmeventd
- docker
- cleanup
---

In one of my projects we recently reached very high development velocity, which lead to a lot of new docker image versions being deployed, which in turn lead to (ECS) docker engines eating up CPU cycles through dmeventd.
A quick look at /var/log/messages offered some lines in which dmeventd was complaining about missing disk space. That's when it dawned on me: Our CIS (strider) didn't clean up excited docker containers neither it removed old docker images after it deployed a new version of a container image and spun up new containers from it :-(

The following 2 lines will help you clean up your docker engines manually and can also be included in your deploy script to do this every time a new docker image version was deployed:

Remove excited containers:
`sudo docker rm $(docker ps -q -f status=exited)`

Remove dangling (un-tagged) images:
`sudo docker rmi $(docker images -f "dangling=true" -q)`