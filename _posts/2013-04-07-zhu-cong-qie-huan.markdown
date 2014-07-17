---
layout: post
title: "主从切换"
date: 2013-04-07 20:32
comments: true
sharing: true
footer: true
categories: [数据存储]
---

1个master，1个slave1，1个slave2，关闭master，让slave1做master，slave2同步新master

+ slave1开启同步账号

{% highlight bash %}
mysql > grant replication slave on *.* to 'backup'@'192.168.0.152' identified by '123456';
mysql > grant replication slave on *.* to 'backup'@'192.168.0.153' identified by '123456';
mysql > flush privileges;
{% endhighlight %}

+ 锁住master的写

{% highlight bash %}
mysql > flush tables with read lock;

# 关闭锁的命令：unlock tables;
{% endhighlight %}

<!-- more -->

+ 查看slave1和slave2的同步状态

{% highlight bash %}
mysql > show processlist;

# 确保 Slave has read all relay log; waiting for the slave I/O thread to update it
{% endhighlight %}

+ 修改slave1的配置，并重启

{% highlight bash %}
bind-address = 0.0.0.0

$ sudo service mysql restart
{% endhighlight %}

+ 停止slave1的slave，设置为master

{% highlight bash %}
mysql > stop slave;
mysql > reset master;
{% endhighlight %}

+ 停止slave2的slave，重新设置master

{% highlight bash %}
mysql > stop slave;

mysql > change master to
      > master_host = '192.168.0.151',
      > master_user = 'backup',
      > master_password = '123456';

mysql> start slave;
{% endhighlight %}

+ 测试是否成功

{% highlight bash %}
mysql > create table `test` ( id int not null auto_increment, `name` varchar(100) not null, primary key (`id`) );
mysql > drop table test;

{% endhighlight %}
