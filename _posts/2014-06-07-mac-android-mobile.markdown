---
layout: post
title: "mac 下识别android手机"
date: 2014-06-07 22:53
comments: true
sharing: true
footer: true
categories: [移动]
---

关于本机->更多信息->概系统览->系统报告->usb->你所连接的device->供应商ID(Vendor ID)

![Vendor ID](/images/post/adb.jpg)

设置vendor id，然后重启

{% highlight bash %}
echo "0x04e8" > ~/.android/adb_usb.ini
./adb kill-server
./adb start-server
{% endhighlight %}

看下 android device bridge 里面的设备有了没，有就对了

{% highlight bash %}
./adb devices

List of devices attached
0019aed7047b5e  device
{% endhighlight %}
