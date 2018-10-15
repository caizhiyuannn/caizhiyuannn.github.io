---
title: "Linux 上一些软件包记录"
date: <span class="timestamp-wrapper"><span class="timestamp">&lt;2018-10-14 Sun 03:50&gt;</span></span>
layout: post
categories: 
- linux
tags: 
- linux 
- packages
---

# Table of Contents

1.  [linux 上的一些软件包](#org4301a03)
    1.  [ASCII 输出文字的软件](#org2a864e2)


<a id="org4301a03"></a>

# linux 上的一些软件包


<a id="org2a864e2"></a>

## ASCII 输出文字的软件

-   **COWSAY**
    
    cowsay, 通过一个小奶牛把需要显示的文字输出到屏幕上。
    
    {% highlight sh %}
    # 安装cowsay
    # sudo apt-get install cowsay
    cowsay "hello world"
    
    {% endhighlight %}
    
    RESULTS:
    
         ______________
        < mewbies rule >
         --------------
                \   ^__^
                 \  (oo)\_______
                    (__)\       )\/\
                        ||----w |
                        ||     ||

-   **XCOWSAY**
    
    xcowsay 为gui模式版的cowsay。

-   **TOILET**
    
    toilet, 通过libcaca一个图形库输出ASCII文本，具有颜色的特性.
    
    {% highlight sh %}
    toilet "Mewbies"
    {% endhighlight %}
    
    RESULTS:
    
                             #        "
        m mm    mmm  m     m #mmm   mmm     mmm    mmm
        #"  #  #"  # "m m m" #" "#    #    #"  #  #   "
        #   #  #""""  #m#m#  #   #    #    #""""   """m
        #   #  "#mm"   # #   ##m#"  mm#mm  "#mm"  "mmm"
        
        ▄    ▄        ▀▀█    ▀▀█                                       ▀▀█        █
        █    █  ▄▄▄     █      █     ▄▄▄         ▄     ▄  ▄▄▄    ▄ ▄▄    █     ▄▄▄█
        █▄▄▄▄█ █▀  █    █      █    █▀ ▀█        ▀▄ ▄ ▄▀ █▀ ▀█   █▀  ▀   █    █▀ ▀█
        █    █ █▀▀▀▀    █      █    █   █         █▄█▄█  █   █   █       █    █   █
        █    █ ▀█▄▄▀    ▀▄▄    ▀▄▄  ▀█▄█▀          █ █   ▀█▄█▀   █       ▀▄▄  ▀█▄██

-   **FIGLET**
    
    figlet, -w 为显示的宽度（字符），-f 可以定义不同的字体样式，-c 使生成的 ASCII 艺术字居中显示。
    
    {% highlight sh %}
    figlet -f slant "hello world"
    {% endhighlight %}
    
    RESULTS:
    
            __         ____                         __    __
           / /_  ___  / / /___ _      ______  _____/ /___/ /
          / __ \/ _ \/ / / __ \ | /| / / __ \/ ___/ / __  /
         / / / /  __/ / / /_/ / |/ |/ / /_/ / /  / / /_/ /
        /_/ /_/\___/_/_/\____/|__/|__/\____/_/  /_/\__,_/

-   **FORTUNE**
    
    Fortune, 会随机输入一句格言。
    
    {% highlight sh %}
    fortune -s
    {% endhighlight %}
    
    RESULTS:
    
        Did you know that if you took all the economists in the world and lined
        them up end to end, they'd still point in the wrong direction?

-   **BOXES**
    
    boxes, 输出ascii文字被包围在图案的里面
    
    {% highlight sh %}
    figlet -f slant mewbies | boxes -d peek -pa2t0b0
    {% endhighlight %}
    
    RESULTS:
    
        /*       _\|/_
        (o o)
        +----oOO-{_}-OOo---------------------------------+
        |                             __    _            |
        |     ____ ___  ___ _      __/ /_  (_)__  _____  |
        |    / __ `__ \/ _ \ | /| / / __ \/ / _ \/ ___/  |
        |   / / / / / /  __/ |/ |/ / /_/ / /  __(__  )   |
        |  /_/ /_/ /_/\___/|__/|__/_.___/_/\___/____/    |
        |                                                |
        +-----------------------------------------------*/

-   **DITAA**
    
    ditaa, 将ascii 符号转换成png格式的图像，需要java的支持。
    
    {% highlight ditaa %}
    +-----------+         +----------+
    |           |         |          |
    |   PLC     <--------->    PLC   |
    |  Network  |         |    c707  |
    |   cRED    |         |          |
    +-----------+         +-+--------+
                            |
                            |
               +------------+
               |
         +-----v------+             +-------------+             +-------------+
         |            |             |  Shared     |             |             |
         |  Database  +------------->  {d} cGRE   +-------------> Executive   |
         |  c707      |             |             |             |  c707       |
         +------------+             +-------------+             +-------------+
    
    {% endhighlight %}
