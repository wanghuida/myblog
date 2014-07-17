---
layout: post
title: "ubuntu keychain 使用"
date: 2013-07-18 22:33
comments: true
sharing: true
footer: true
categories: [系统]
---


+ `ssh-keygen`生成密钥，经常会设置一个密码，让试图窃取的人无计可施。
+ 问题来了，每次登录都会要求输入密码，是时候来搞个`keychain`了



{% highlight bash %}
$ sudo apt-get install keychain
$ /usr/bin/keychain ~/.ssh/id_rsa

# 加到.profile
. ~/.keychain/$HOSTNAME-sh
. ~/.profile


{% endhighlight %}

+ keychain到底干了什么呀？

keychain会起一个`ssh-agent`，后来登录的人通过`$HOSTNAME-sh`设置环境变量使用同一个`ssh-agent`




