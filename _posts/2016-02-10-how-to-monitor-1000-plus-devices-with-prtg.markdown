---
title: How to monitor 1000+ devices with PRTG
date: 2016-02-10 15:21:00 -08:00
tags:
- prtg
- snmp
- core
- scale
---

![webgui-new-device.png](/uploads/webgui-new-device.png)

I recently had the pleasure to implement PRTG in an environment with 1000+ devices in a larger organization. This article summarizes what I learned and is supposed to give you ideas about what works and what doesn’t work for similar projects.

**How to scale PRTG**

Lets start with the design of the server infrastructure that runs the various PRTG services. In general PRTG consists of the following components:

* PRTG Core Server - Provides the database, API and web interface of the PRTG product.
* PRTG Local Probe - A service that polls and receives monitoring data from your devices and runs on a PRTG Core Server.
* PRTG Remote Probe - A service that polls and receives monitoring data from your devices and runs on a Windows host other than a PRTG Core Server.
* PRTG Mini Probes - Services that poll and receive monitoring data from your devices and run on none-Windows hosts.

In addition to just using the components above by themselves you can also cluster PRTG Core Servers to achieve redundancy. Depending on your network design and operational requirements a PRTG cluster allows you to preserve some kind of visibility into your IT infrastructure during bigger outages. The PRTG manual includes an excellent article about its clustering feature here ([https://www.paessler.com/manuals/prtg/clustering](https://www.paessler.com/manuals/prtg/clustering)).
In order to come up with a lasting architecture that does not break down the moment someone on your team adds a couple of hundred sensors you should consider the following:


* PRTG cluster nodes do not scale very well, each additional cluster node will consume resources that you might need for processing sensor data later.
* PRTG is a very CPU heavy service, so be careful virtualizing PRTG Core Servers. If you absolutely need to virtualize it, do not go overboard with vCPUs (see [SMP VMs](http://vbrainstorm.com/one-two-or-four-vcpus-in-vmware/)).
* PRTG Remote Probes can be virtualized without pain, if you distribute the amount of sensors evenly between them - Try to stay under 2500 sensors per Remote Probe.
* It can be helpful to not use the Local Probes on your PRTG Core Servers to monitor other devices at all. Use Remote Probes instead.
* Plan according to your expected usage of sensor types. ([Read here!](https://kb.paessler.com/en/topic/2733-how-can-i-speed-up-prtgespecially-for-large-installations))

In this last PRTG setup we used 2 clustered PRTG Core Servers and 7 PRTG Remote Probes to distribute the load of ca. 8000 sensors. Some of the Remote Probes are fairly under-utilized though, so you could definitely get away with just 4 Remote Probes.

**How to on-board a lot of devices and sensors to PRTG**

There are generally 3 ways of on-boarding devices and sensors in PRTG:

* Manually add each and every device
* Use the Auto-Discovery feature
* Leverage the PRTG API

In a large environment the manual option will take a while, so you want to focus on how to leverage the Auto-Discovery feature or/and the PRTG API.
Which one of these 2 options will be more successful in a particular project depends on how well the device population is organized. If you have great structure in AD, you could leverage that through the Auto-Discovery feature. If you have meaningful separation through IP subnets the Auto-Discovery feature is your friend as well. If you have good inventory lists but nothing else, you might want to feet CSV files into scripts that call the PRTG API to create your devices in the device tree.

In order to effectively use the Auto-Discovery feature you should invest some time into creating meaningful device templates. But keep in mind that while device templates work great with (Windows) servers they don't work so well with multiple types of network devices like switches and routers.

**Some words about SNMP**

You will want to use SNMP to monitor a lot of devices because it is cheap in resources. Depending on your device population you will have less or more work to setup SNMP monitoring. Here are two tools that are helpful:

* [SNMP MIB Importer](https://www.paessler.com/tools/mibimporter)
* [PS script to install and configure SNMP on Windows servers](https://community.whatsupgold.com/?signin&r=%2flibrary%2fpowershellscripts%2finstallandconfiguresnmpwithpowershell)

**How to customize the PRTG user experience**

To make the lives of new PRTG users easier, you might want to set the user's homepage to a default through their associated user groups. You might also want to give permissions on the device subtree that is relevant to the user, so she doesn't have to go hunt for her devices in the global device tree.
Also make use of PRTG libraries to build summarizing views for applications that spread their services over multiple Remote Probes (Active Directory is a great example for that).

**API + Powershell**

If you use the Auto-Discovery feature to add a lot of devices, you will end up with meaningless sensor names. This makes life harder if you use libraries to build yourself application/service based views. A great way to get meaningful sensor names really quickly is using the [PRTG API](https://prtg.paessler.com/api.htm?username=demo&password=demodemo&tabid=1).

I ended up writing a Powershell PRTG API wrapper to make calling the API via Powershell quick and easy. You can find my code on [Github](https://github.com/bersfo/prtg-api-wrapper).

If you know about other best practices, please don't hesitate to comment on this post.