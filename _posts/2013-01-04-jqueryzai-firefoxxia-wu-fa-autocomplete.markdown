---
layout: post
title: "jquery在firefox下无法autocomplete"
date: 2013-01-04 17:29
comments: true
sharing: true
footer: true
categories: [前端]
---

#### jquery的autocomplete中文输入在firefox无法正常使用

+ firefox下用input事件触发keydown即可

{% highlight javascript %}
$('元素').bind('input', function(){
    $(this).trigger('keydown');
}).bind("keydown", function(event){
    事件
}
{% endhighlight %}
