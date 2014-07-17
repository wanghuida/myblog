---
layout: post
title: "AngularJS 初探"
date: 2014-07-16 10:37
comments: true
sharing: true
footer: true
categories: [前端]
---

先看个例子，只引用了AngularJS，没有写任何js

<iframe width="100%" height="300" src="http://jsfiddle.net/wanghuida/Zcer7/1/embedded/result,js,html,css" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

{% highlight html %}
<div ng-app="">
    <label>名字:</label>
    <input type="text" ng-model="username" placeholder="Enter a name here" />
    <hr />
    <h1>你好 {{username}}!</h1>
</div>
{% endhighlight %}

+ ng-app定义angular的作用范围
+ ng-model采用数据绑定，这里绑定username
+ {{ username }}根据数据绑定，自动更改username
