---
layout: post
title: "ubuntu 服务器基础配置"
date: 2013-02-26 12:58
comments: true
sharing: true
footer: true
categories: [系统]
---

### 配置.profile

{% highlight bash %}
export EDITOR=vim

# set terminal color
PS1='\[\e[1;32m\]\u\[\e[m\]@' # user
PS1=$PS1'\[\e[1;31m\]\h\[\e[m\] ' # host
PS1=$PS1'\[\e[1;34m\]\W\[\e[m\] ' # wd
#PS1=$PS1'\[\e[1;33m\]$(__ruby_version)\[\e[m\] ' # rvm version
#PS1=$PS1'\[\e[1;32m\]$(__git_ps1)\[\e[m\] ' # git
export PS1 

{% endhighlight %}

<!-- more -->


### 配置.vimrc

{% highlight bash %}
set nocompatible
set backspace=2
 
set nu
syntax on
 
set autoindent
set softtabstop=4
set tabstop=4
set shiftwidth=4
set expandtab
 
set showmatch
set ruler
 
filetype plugin on
set laststatus=2
set encoding=utf-8
set hlsearch
set showcmd
 
set scrolloff=4
set ignorecase smartcase
 
{% endhighlight %}

### 配置sudo

{% highlight bash %}
visudo 
# 请放在最下面
wanghuida   ALL=(ALL) NOPASSWD:ALL
{% endhighlight %}

### 配置ssh

{% highlight bash %}
sudo apt-get install ssh

sudo vim /etc/ssh/sshd_config
PasswordAuthentication no

sudo /etc/init.d/ssh restart

mkdir .ssh
chmod 700 .ssh
cd ssh
touch authorized_keys
# 增加pub key进去就可以了
{% endhighlight %}
