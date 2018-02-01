---
title: How to create meaningful AWS Cloudwatch dashboards
date: 2016-03-04 15:34:00 -08:00
tags:
- aws
- cloudwatch
- best practice
- dashboard
- charts
- widgets
---

No matter what workload you run in AWS' various cloud offerings, you usually want to know how your services are behaving in that cloud. Luckily AWS Cloudwatch offers a pretty sleek dashboard that allows you to create web-based dashboards showing all kinds of metrics in line graphs. (Unfortunately line graph is the only type of graphs that was supported as of this writing.)
In this post I documented how to use CloudWatch to quickly produce meaningful dashboards so you can start analyzing the behavior of your workloads.

Before we start let me remind you quickly that Cloudwatch has some small costs associated to its usage. Please visit [https://aws.amazon.com/cloudwatch/pricing/](https://aws.amazon.com/cloudwatch/pricing/) for the details.

OK, now lets start with a goal:
![xcw-dashboard-example-1.png](/uploads/xcw-dashboard-example-1.png)

We want to create a dashboard that helps the viewer to easily understand what is going on in her AWS solution.

First go to the Cloudwatch Console and click on Dashboards in the main menu on the left. Then just hit the big blue "Create dashboard" button to create your first dashboard. Give it a name and hit that blue button again - Voila! Here you have your first (empty) dashboard:
![xcw-dashboard-start.png](/uploads/xcw-dashboard-start.png)

So now go ahead and add your first Metric graph by clicking on "Configure". The next thing you will se is the "Add graph" wizard, which gives you a menu of Metrics by Category.
![xcw-dashboard-metrics.png](/uploads/xcw-dashboard-metrics.png)

Depending on your existing workloads and custom metrics that you have configured, this menu has less or more items to show.
Assuming you have some kind of EC2 workload running in you account, please go ahead and click on "EC2 Metrics". This will bring up the next screen of the "Add Graph" dialog and lists the first 200 metrics that are available in this category for your account. So you might have to refine your search or use the various links in the search results (As an example I usually click on instance-IDs to get a listing of all metrics that are available for that specific instance.) to find what you want. Once you found what you are interested in, toggle the checkbox in front of the metric.
![xcw-dashboard-addmetric.png](/uploads/xcw-dashboard-addmetric.png)

Now you could just hit the "Create widget" button or you customize your chart a bit by dragging up the chart area.
![xcw-dashboard-chart.png](/uploads/xcw-dashboard-chart.png)

Depending on your metrics, you might want to change the name of the graph (1), the aggregation function (2) or the left and right Y-axis (3)(4). This step ist often overlooked and lets the user end up with a not so meaningful chart. Here is an example of a customized vs a default settings chart:
![xcw-dashboard-chart2.png](/uploads/xcw-dashboard-chart2.png)

Alright, now you are able to create meaningful charts. Lets get into placing those charts on the dashboard. You might have already noticed that you can drag charts around to place them in a meaningful order. (Just mouse-over the title area of the chart you'd like to drag around.)
In addition you can also change the size of the charts, which gives you some wiggle room to emphasize certain metrics. Here is an example on how to use these 2 features:
![xcw-dashboard-chart3.png](/uploads/xcw-dashboard-chart3.png)

In addition there is also a pretty handy Text-Widget available to add some more meaning to your dashboard. I tend to text-widgets to separate the functional layers of the solutions I'm working on - Here is an example:
![xcw-dashboard-example.png](/uploads/xcw-dashboard-example.png)

The text-widget I used in the example above has the following content:
![xcw-dashboard-textwidget.png](/uploads/xcw-dashboard-textwidget.png)

That is it! All you need to know to create some meaningful AWS Cloudwatch dashboards. Additional info can be found here: [https://aws.amazon.com/blogs/aws/cloudwatch-dashboards-create-use-customized-metrics-views/](https://aws.amazon.com/blogs/aws/cloudwatch-dashboards-create-use-customized-metrics-views/)

