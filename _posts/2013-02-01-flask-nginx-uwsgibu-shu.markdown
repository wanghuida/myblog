---
layout: post
title: "flask nginx uwsgi 部署"
date: 2013-02-01 14:10
comments: true
sharing: true
footer: true
categories: [后端]
---

### 安装 uwsgi

{% highlight bash %}
$ brew install uwsgi
{% endhighlight %}

### 安装 nginx

{% highlight bash %}
$ brew install nginx 
{% endhighlight %}

### 配置Flask环境

{% highlight bash %}
$ mkdir test
$ cd test
$ virtualevn sandbox
$ . sandbox/bin/activate
$ pip install Flask
{% endhighlight %}

<!-- more -->

### 创建一个Flask项目

    $ touch test.py

{% highlight python %}
# 内容如下

from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello():
    return 'Hello World'

if __name__ == '__main__':
    app.run()

{% endhighlight %}

### 创建uwsgi配置文件

{% highlight bash %}
$ touch test_config.xml

<uwsgi>
    <pythonpath>/Users/william/project/test</pythonpath>
    <module>test</module>
    <callable>app</callable>
    <socket>/tmp/uwsgi.sock</socket>
    <master/>
    <processes>4</processes>
    <memory-report/>
</uwsgi>

{% endhighlight %}

### nginx 配置

{% highlight bash %}

server {
    listen 80;
    server_name www.test.com;

    location / {
        include uwsgi_params;
        uwsgi_pass unix:/tmp/uwsgi.sock; 
    }
}
{% endhighlight %}

### 启动服务

{% highlight bash %}
sudo nginx -s reload

# 支持virtualenv, uswgi还可以--py-auto-reload
sudo uwsgi -x /Users/william/project/test/test_config.xml --virtualenv sandbox 
{% endhighlight %}

