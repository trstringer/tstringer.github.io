---
layout: post
title:  "Set a Static IP Address on a Raspberry Pi (Raspbian Jessie)"
date:   2016-03-08 08:00
categories: raspberrypi iot raspbian linux 
---
I was recently wrestling with this one.  I was in need of setting a static IP address for my Rasperry Pi (running Raspbian Jessie).  I kept trying to play around with `/etc/network/interfaces` but no configuration changes there were "working".

Then I actually read the comments in `/etc/network/interfaces` ... `For static IP, consult /etc/dhcpcd.conf and 'man dhcpcd.conf'`.  So then I rolled back all of changes I made to `interfaces` and added the following to `dhcpcd.conf` file...

```
interface eth0

static ip_address=<ip-address>/<subnet-prefix-length>
static routers=<router-ip-address>
static domain_name_servers=<dns-ip-address>
```

After I made these changes and rebooted, my RPi was now listening on my desired and configured static IP address.

Enjoy!