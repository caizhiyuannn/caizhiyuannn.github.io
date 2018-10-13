---
title: "启用apache2 动态网页的支持"
date: <span class="timestamp-wrapper"><span class="timestamp">&lt;2016-07-01 Fri&gt;</span></span>
layout: post
categories: 
- linux
tags: 
- apache 
- cgi-bin
---

# Table of Contents

1.  [配置cgi 模块开启shell 执行功能](#org7d19df3)
2.  [快速配置方法](#orge9b9a52)
3.  [注意细节。](#orgee18177)
4.  [具体shell 示例](#orgf0c371f)
5.  [serve-cgi-bin.conf 改动地方示例](#orgfc2febc)


<a id="org7d19df3"></a>

# 配置cgi 模块开启shell 执行功能

1.  开启cgi 模块。
    -   /usr/sbin/a2enmod cgi    &#x2014;>  可以使用默认环境不加前缀

2.  修改 cgi-bin 的配置文件 /etc/apache2/conf-enabled/serve-cgi-bin.conf
    -   配置ScriptAlias指定/var/www/cgi-bin/目录存放cgi程序，并映射到网站根目录。
    -   指定/var/www/cgi-bin目录进行授权访问以及开放ExecCgi 的权限

3.  配置Handler 指定文件识别为cgi-bin 的可执行文件
    -   AddHandler cgi-script .cgi .pl .sh
    -   (cgi-script 可以名字随意， 后面是可执行后缀识别)

4.  设置Handler 识别 ，在 <directory "*var/www/cgi-bin*"> 里面配置
    -   SetHandler cgi-script  （主要是引用第3步设置的Handler，进行识别）

5.  配置/var/www/cgi-bin目录以及shell文件的权限，所有者为www-data。  
    shell文件必须有执行的权限

6.  重启apache2 服务


<a id="orge9b9a52"></a>

# 快速配置方法

1.  开启cgi 模块。
2.  修改/etc/apache2/apache2.conf 文件 对目录html 进行授权
3.  html 目录 options 选项添加 ExecCGI 允许执行cgi文件
4.  配置ScriptAlias / *var/www/html*  将脚本文件映射到主目录上 。   
    注意：ScriptAlias 所映射的目录后一定要加/

5.  配置目录以及脚本相应的权限
6.  重启服务


<a id="orgee18177"></a>

# 注意细节。

-   shell 等脚本文件输出时必须添加html 头文件  
    "Content-type: text/html" 用来指定网页的类型

-   shell 等脚本文件第一行必须声明执行脚本的语言。如shell为 ： #!/bin/bash


<a id="orgf0c371f"></a>

# 具体shell 示例

{% highlight shell %}
#!/bin/bash
echo -e "Content-type: text-html \n\n"
echo "hello world"
date
{% endhighlight %}


<a id="orgfc2febc"></a>

# serve-cgi-bin.conf 改动地方示例

{% highlight conf %}
<IfModule mod_alias.c>
  ScriptAlias /cgi-bin/ /var/www/cgi-bin/
  <Directory "/var/www/cgi-bin/">
      AllowOverride None
      Options +ExecCGI -MultiViews +SymLinksIfOwnerMatch
      Require all granted
  </Directory>
</IfModule>
{% endhighlight %}
