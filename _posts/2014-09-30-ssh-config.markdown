---
layout: post
title: "ssh_config 占位符"
date: 2014-09-30 22:28
comments: true
sharing: true
footer: true
categories: [系统]
---

+ 一般会有多台机器需要登录，通常会如下配置

{% highlight bash %}

Host idc01-001
hostname 192.168.0.1
user ubuntu

Host idc01-002
hostname 192.168.0.2
user ubuntu

Host idc01-003
hostname 192.168.0.3
user ubuntu

{% endhighlight %}

+ 上面如果有100台机器就要配置100个，真是弱爆了，还是来学习一种高档配置吧

{% highlight bash %}

Host ???
HostName 192.168.0.%h
user ubuntu

# 直接使用 $ ssh 002 即可登录

{% endhighlight %}


