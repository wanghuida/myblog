---
layout: post
title: "octopress 介绍"
date: 2012-07-07 03:10
comments: true
sharing: true
footer: true
categories: [系统]
---


安装octopress
-----------
>安装一下ruby和rvm

>获取源代码

{% highlight bash %}
rvm install 1.9.2 && rvm use 1.9.2
git clone git://github.com/imathis/octopress.git octopress
gem install bundler
bundle install
rake install
{% endhighlight %}

