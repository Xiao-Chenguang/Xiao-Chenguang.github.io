---
layout: post
title: modify hosts for fast access to github.com
date:   2024-01-04
categories: skills
author: Chenguang Xiao
---

Github is a great platform for open source projects. However, the access to github.com is not always fast. In this post, I will show how to modify the hosts file to speed up the access to github.com in China.

There are two steps to achieve this:
1. Find the fast IP address of github.com
2. Add it to the hosts file

## Find the fast IP address of github.com
You can check the latency of github.com in [this page](https://tool.chinaz.com/dns/GitHub.com).
Then chose one or more IP addresses with the lowest latency.

## Add it to the hosts file
The hosts file is located at `/etc/hosts` in Linux and Mac OS. You can use `sudo vim /etc/hosts` to edit it.
Add the IP address and the domain name to the hosts file. For example, it will look like this:
```
20.205.243.166 github.com
140.82.121.4 github.com
```

## Check the result
You can use `ping github.com` to check the IP address of github.com. It should be the one you added to the hosts file.
Directly access github.com in the browser to check if it is faster.