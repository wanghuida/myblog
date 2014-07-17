---
layout: post
title: "hive 读取nginx 日志"
date: 2014-05-22 17:35
comments: true
sharing: true
footer: true
categories: [后端]
---

安装完hive 跑map reduce会显示下面的错误

{% highlight java %}
Caused by: java.lang.ClassNotFoundException: Class org.apache.hadoop.hive.contrib.serde2.RegexSerDe not found
    at org.apache.hadoop.conf.Configuration.getClassByName(Configuration.java:1626)
    at org.apache.hadoop.hive.ql.exec.MapOperator.getConvertedOI(MapOperator.java:305)
    ... 24 more
{% endhighlight %}

+ 可以加入jar包解决

{% highlight java %}
add jar <relative-classpath or absolute-classpath>/hive-contrib-0.13.0.jar
{% endhighlight %}

+ 设置nginx access_log日志格式

{% highlight java %}
    log_format  main '$request_time $upstream_response_time $remote_addr $request_length $upstream_addr  [$time_local] '
                     '$host "$request" $status $bytes_sent '
                     '"$http_referer" "$http_user_agent" "$gzip_ratio" "$http_x_forwarded_for" - "$server_addr"';
{% endhighlight %}

<!-- more -->

+ 用正则按格式创建表

{% highlight java %}
create external table lblog (
request_time string,
upstream_response_time string,
remote_addr string,
upstream_addr string,
time_local string,
host string,
method string,
request_url string,
request_schema string,
status string,
bytes_sent string,
http_referer string,
http_user_agent string,
gzip_ratio string,
http_x_forwarded_for string,
server_addr string
)
partitioned by (ds string)
row format serde 'org.apache.hadoop.hive.contrib.serde2.RegexSerDe'
with serdeproperties ('input.regex' = '(.*)\\s(.*)\\s(.*)\\s-\\s(.*)\\[(.*)\\]\\s(.*)\\s\"(.*)\\s(.*)\\s(.*)\"\\s(.*)\\s(.*)\\s\"(.*)\"\\s\"(.*)\"\\s\"(.*)\"\\s\"(.*)\"\\s-\\s\"(.*)\"','output.format.string' = '%1$s %2$s %3$s %4$s %5$s %6$s %7$s %8$s %9$s %10$s %11$s %12$s %13$s %14$s %15$s %16$s')
location '/lblog';
{% endhighlight %}

+ 现在是查不到数据库的，必须add partition

{% highlight java %}
alter table testlblog5 add partition (ds='20140519');
{% endhighlight %}
