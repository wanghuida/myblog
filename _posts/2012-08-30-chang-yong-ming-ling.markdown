---
layout: post
title: "常用命令"
date: 2012-08-30 13:14
comments: true
sharing: true
footer: true
categories: [系统]
---

###过滤记录

+ -l自动chomp，结果加$/
+ -a自动分割

{% highlight bash %}
tail -f access-2012-08-30.log | grep -v '*' \ 
    | perl -w -lane '$a = $F[@F-1];print if $a > 50000 '

{% endhighlight %}

###获取URL内容
+ -I 获取头信息
+ -x 通过哪台服务器
+ -A 设置user agent,可以让log过滤更方便

{% highlight bash %}
curl -I -x 127.0.0.1  "http://test/abc.jpg" -A "huida"
{% endhighlight %}

###批量删除一天以前的文件

{% highlight bash %}
find /dev/shm/ -type f -mtime +1 | xargs rm
{% endhighlight %}

###计算tcp连接数

{% highlight bash %}
su -
netstat -lant | wc -l
{% endhighlight %}


###增加网关
+ mac版

{% highlight bash %}
sudo route add -net 10.0.0.0/8 -interface ppp0
{% endhighlight %}

###格式化和mount磁盘
+ xfs系统

{% highlight bash %}
/sbin/mkfs.xfs /dev/sdb
mount –t xfs /dev/sdb /data1
vim /etc/fstab
umount -l /tmp/
{% endhighlight %}

###导出数据
+ -h -u -p表示主机，用户，密码
+ -D表示数据库
+ -e表示执行语句
+ -N表示跳过列名, --skip-column-names
+ -s表示用tab分割字段, --silent,Be more silent. Print results with a tab as separator, each row on new line.

{% highlight bash %}
mysql -h -u -p -Ns -Ddatabase -e "select * from ~~~ where ~~~" > /tmp/fid
{% endhighlight %}


###远程取得数据

{% highlight bash %}
sftp
scp
rsync
{% endhighlight %}

###查看系统状况

{% highlight bash %}
iostat -x 1
free -m
w
top
ping
lsof -i4TCP -P
netstat -lnp
{% endhighlight %}
