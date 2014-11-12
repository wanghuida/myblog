---
layout: post
title: "DOM头惹的祸"
date: 2014-09-30 22:28
comments: true
sharing: true
footer: true
categories: [后端]
---


解析json 返回 `JSON_ERROR_SYNTAX`，api端返回正常

{% highlight php %}

<?php

// $result 为 null
$result = json_decode($json);

// 返回 JSON_ERROR_SYNTAX
$reason = json_last_error();

{% endhighlight %}


经过查找原始阿里文件服务的php 带有DOM导致解析失败，下面是一个查找dom头的命令

{% highlight bash %}

find -type f | while read file;do [ "`head -c3 -- "$file"`" == $'\xef\xbb\xbf' ] && echo "found BOM in: $file";done

{% endhighlight %}
