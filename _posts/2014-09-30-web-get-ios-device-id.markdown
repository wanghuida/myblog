---
layout: post
title: "web 取得ios设备的DeviceId"
date: 2014-09-30 22:28
comments: true
sharing: true
footer: true
categories: [移动]
---

+ 用普通的方法想要在safari中获取DeviceId基本是不可能的，下面介绍一种特殊的方法


创建一个获取结果的php文件，result.php

{% highlight php %}
<?php
// result.php

$result = file_get_contents('php://input');
file_put_contents('/tmp/result.txt', $result);
?>
{% endhighlight %}



创建一个html文件 index.html 读取m.mobileconfig文件

{% highlight html %}
<!-- index.html -->
<a href="/m.mobileconfig">安装证书</a>
{% endhighlight %}



创建m.mobileconfig，记得更改成自己URL

{% highlight xml %}
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple Computer//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
    <dict>
        <key>PayloadContent</key>
        <dict>
            <key>DeviceAttributes</key>
            <array>
                <string>UDID</string>
                <string>IMEI</string>
                <string>MEID</string>
                <string>ICCID</string>
                <string>VERSION</string>
                <string>PRODUCT</string>
                <string>MAC_ADDRESS_EN0</string>
                <string>DEVICE_NAME</string>
                <string>DeviceName</string>
                <string>SERIAL</string>
                <string>IMSI</string>
                <string>Model</string>
                <string>ModelName</string>
                <string>OSVersion</string>
                <string>WiFiMAC</string>
            </array>
            <key>URL</key>
            <string>http://localhost/result.php</string>
        </dict>
        <key>PayloadDescription</key>
        <string>Just collect something sensitive.</string>
        <key>PayloadDisplayName</key>
        <string>Device Attribute Collection</string>
        <key>PayloadIdentifier</key>
        <string>com.sskaje.profile-service</string>
        <key>PayloadOrganization</key>
        <string>sskaje.me</string>
        <key>PayloadType</key>
        <string>Profile Service</string>
        <key>PayloadUUID</key>
        <string>3C9C7688-1655-4603-8761-960409082944</string>
        <key>PayloadVersion</key>
        <integer>1</integer>
    </dict>
</plist>
{% endhighlight %}


赶紧打开html文件点击链接试试吧，/tmp/result.txt的结果应该如下

{% highlight xml %}
<plist version="1.0">
<dict>
    <key>IMEI</key>
    <string>01 200321 834020 4</string>
    <key>PRODUCT</key>
    <string>iPhone4,1</string>
    <key>SERIAL</key>
    <string>C39GD4MGWTDD</string>
    <key>UDID</key>
    <string>512aabdcsd92624fa8317e650da7bb3b44cadebf</string>
    <key>VERSION</key>
    <string>12A365</string>
</dict>
</plist>
{% endhighlight %}
