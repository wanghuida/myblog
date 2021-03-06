---
layout: post
title: "OAuth 介绍"
date: 2012-07-13 13:01
comments: true
sharing: true
footer: true
categories: [系统]
---


###在认证和授权的过程中涉及的三方包括：


+ 服务提供方 (Service Provider)，用户使用服务提供方来存储受保护的资源，如照片，视频，联系人列表。
+ 用户 (User)，存放在服务提供方的受保护的资源的拥有者。
+ 客户端 (Client)，要访问服务提供方资源的第三方应用，通常是网站，如提供照片打印服务的网站。在认证过程之前，客户端要向服务提供者申请客户端标识。

###使用OAuth进行认证和授权的过程如下所示:

1. 用户访问客户端的网站，想操作用户存放在服务提供方的资源。
1. 客户端向服务提供方请求一个临时令牌 (Request Token)。
1. 服务提供方验证客户端的身份后，授予一个临时令牌。
1. 客户端获得临时令牌后，将用户引导至服务提供方的授权页面请求用户授权。在这个过程中将临时令牌和客户端的回调连接发送给服务提供方。
1. 用户在服务提供方的网页上输入用户名和密码，然后授权该客户端访问所请求的资源。
1. 授权成功后，服务提供方引导用户返回客户端的网页。
1. 客户端根据临时令牌从服务提供方那里获取访问令牌 (Access Token)。
1. 服务提供方根据临时令牌和用户的授权情况授予客户端访问令牌。
1. 客户端使用获取的访问令牌访问存放在服务提供方上的受保护的资源。

###图例说明
![OAuth](/images/post/oauth_flow.png "OAuth 图例说明")





