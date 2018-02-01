---
title: EC2 memory usage stats aren't working in Cloudwatch after cloning instance
date: 2016-06-05 15:51:00 -07:00
tags:
- cloudwatch
- ec2
- mon-put-instance-data.pl
- instance-id
- memory
---

Today I had to clone an EC2 instance, which hosts a database because AWS informed me that they need to retire the source instance.
After a successful clone/replacement I noticed that the memory stats in our Cloudwatch dashboard still showed up with its old instance ID. A quick Google search offered: [http://serverfault.com/questions/571597/cloudwatch-mon-put-instance-data-not-reporting-on-ami-cloned-instance](http://serverfault.com/questions/571597/cloudwatch-mon-put-instance-data-not-reporting-on-ami-cloned-instance)

In short: You have to remove `/var/tmp/aws-mon/instance-id` from your image, so that the cloudwatch script picks up the correct instance ID.