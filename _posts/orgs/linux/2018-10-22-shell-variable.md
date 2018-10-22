---
title: "SHELL中的变量拓展"
date: <span class="timestamp-wrapper"><span class="timestamp">&lt;2018-10-22 Mon 17:48&gt;</span></span>
layout: post
categories: 
- linux
tags: 
- linux 
- shell
---

# Table of Contents

1.  [SHELL中变量拓展](#org62244c3)
    1.  [字符串切割](#org0d247e5)
        1.  [字符串删除](#org8cf2f04)
    2.  [统计字符串长度](#org006f816)
    3.  [替换或删除操作](#org4a63635)
    4.  [获取变量名](#org3077d1b)
    5.  [指定变量默认值](#org3615373)


<a id="org62244c3"></a>

# SHELL中变量拓展


<a id="org0d247e5"></a>

## 字符串切割

1.  指定开始位置，截取到字符串结束
    
    {% highlight bash %}
    # 格式：${var:index}
    
    var="hello1234"
    echo ${var:5}
    
    {% endhighlight %}
    
        1234

2.  指定开始位置和长度来截图字符串
    
    {% highlight bash %}
    # 格式： ${var:index:length}
    
    var="hello1234"
    
    echo ${var:0:5}
    {% endhighlight %}
    
        hello


<a id="org8cf2f04"></a>

### 字符串删除

    # 删除左边字符串
    % 删除右边字符串

1.  最小删除
    匹配到第一个就满足要求执行操作，可以用 `*` 通配符
    
    {% highlight bash %}
    # 格式： ${var#*str} ${var%str*}
    
    string="/tmp/test/dir/file.txt"
    
    # 移除左边第一个 / 
    echo ${string#*/}
    
    # 移除右面第一个 / 后面的内容, * 通配符
    echo ${string%/*}
    
    {% endhighlight %}
    
    | tmp/test/dir/file.txt |
    | /tmp/test/dir |

2.  最大删除
    匹配到最后一个满足要求的地方并执行删除操作， 可以用 `*` 通配符
    
    {% highlight bash %}
    # 格式：${var##*str} ${var%%str*}
    
    var="hellohello12341234"
    
    # 左边开始贪婪匹配，执行移除
    echo ${var##*3}
    
    # 右面开始贪婪匹配，执行移除
    echo ${var%%l*}
    {% endhighlight %}
    
    | 4 |
    | he |


<a id="org006f816"></a>

## 统计字符串长度

{% highlight bash %}
# 格式：${#var}

var="hello1234"
echo ${#var}
{% endhighlight %}

    9


<a id="org4a63635"></a>

## 替换或删除操作

1.  替换一个符合的字符串
    
    {% highlight bash %}
    # 格式：${var/regex/replace}
    
    var="hellohello12341234"
    
    echo ${var/1234/haha}
    {% endhighlight %}
    
        hellohellohaha1234

2.  替换全部符合字符串
    
    {% highlight bash %}
    # 格式： ${var//regex/replace}
    
    var="hellohello12341234"
    
    echo ${var//hello/haha}
    {% endhighlight %}
    
        hahahaha12341234


<a id="org3077d1b"></a>

## 获取变量名

{% highlight bash %}
# 格式： ${!string@}

var="hellohello"
var1="haha"

echo ${!var@}
{% endhighlight %}

    var var1


<a id="org3615373"></a>

## 指定变量默认值

{% highlight bash %}
# 如果变量 var 为空，则使用指定默认值
echo ${var-"变量var为空"}

# 变量 var1 没有声明或者为空，使用指定默认值
echo ${var1:-"变量var1为空"}

# 用默认值取代变量值，无论是否为空
var2="123"
echo ${var2+"变量var2默认值"}

# 用默认值取代变量值，如果变量值为空，则保留空值
var3=""
echo ${var2:+"取代var2值"}
echo ${var3:+"var3值不为空"}

# var4 未声明则使用默认值，通知var4设置未指定默认值
echo ${var4="var4未声明"}

# var3 为空或者未声明，则使用默认值，同时设置var3为指定默认值
echo ${var3:="var3为空或没设置"}

{% endhighlight %}

| 变量var为空 |
| 变量var1为空 |
| 变量var2默认值 |
| 取代var2值 |
| |
| var4未声明 |
| var3为空或没设置 |
