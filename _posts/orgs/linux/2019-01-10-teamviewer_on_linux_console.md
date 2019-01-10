---
title: "安装teamviewer支持Linux终端环境"
date: <span class="timestamp-wrapper"><span class="timestamp">&lt;2019-01-10 Thu 22:26&gt;</span></span>
layout: post
categories: 
- linux
tags: 
- teamviewer
---

# Table of Contents

1.  [系统环境要求](#org81d6b99)
2.  [安装QT（可选）](#org910eea1)
3.  [安装Linux版 TeamViewer](#org8ab2dcd)
4.  [无人值守配置，通过命令行配置](#org2b82dea)


<a id="org81d6b99"></a>

# 系统环境要求

1.  要求Linux 2.6.27内核（应该是2.6.27以上， 官网没有明确说明）
2.  glibc 2.17 （以上？）
3.  Qt环境，建议安装Qt5.6以上(桌面支持，如果不安装GUI可以忽略)

    注意：
    
    console 控制台必须是framebuffer console。 
    
    如果/dev/fb0 不存在的话， 你可能需要配置内核重新引导来支持它！！
    
    如果X server 没有安装或使用的话， 技术上可以忽略对 Qt 安装依赖。（可以不安装QT环境）
    可以使用TAR包代替包管理器来安装。


<a id="org910eea1"></a>

# 安装QT（可选）

官网提供qt安装包需要提供图形界面进行选项，这里提供一个脚本直接进行安装操作

{% highlight bash %}
sudo apt-get install python3-requests p7zip-full wget

wget https://git.kaidan.im/lnj/qli-installer/raw/master/qli-installer.py
chmod -x qli-installer.py

python3 qli-installer.py linux desktop

{% endhighlight %}


<a id="org8ab2dcd"></a>

# 安装Linux版 TeamViewer

通过官网下载安装包。

{% highlight bash %}
sudo apt install ./teamviewer_13.x.yyy_[arch].deb
sudo apt install ./teamviewer_host_13.x.yyy_[arch].deb

# 以上选择其中一个版本安装即可
{% endhighlight %}


<a id="org2b82dea"></a>

# 无人值守配置，通过命令行配置

如果分配设备到账号的话，可以不用设置密码。

{% highlight bash %}
# 查看帮助
teamviewer help

# 查看TeamViewer ID
teamviewer info 

# 设置登陆密码
teamviewer passwd xxx

# 分配设备到账号
teamviewer setup
{% endhighlight %}
