---
title: "emacs<sub>snippet</sub>"
date: <span class="timestamp-wrapper"><span class="timestamp">&lt;2018-10-16 Tue 15:51&gt;</span></span>
layout: post
categories: 
- emacs
tags: 
- emacs 
- yasnippet
---

# Table of Contents

1.  [YASnippet](#org78d7eb2)
    1.  [安装](#org0969a87)
2.  [Snippet 配置](#orgc1df448)
    1.  [快捷键](#org3f949e3)
    2.  [snippet 文件内容](#orgaf0fd5f)


<a id="org78d7eb2"></a>

# YASnippet

YASnippet 是emacs 的一个模板插件，允许键入缩写来拓展模块，补全内容。


<a id="org0969a87"></a>

## 安装

-   使用 `package-install` 安装
    
    {% highlight emacs-lisp %}
    (package-install 'yasnippet)
    (require 'yasnippet)
    ;; 全局模式
    (yas-global-mode 1)
    {% endhighlight %}


<a id="orgc1df448"></a>

# Snippet 配置


<a id="org3f949e3"></a>

## 快捷键

-   `M-x yas-new-snippet` 快捷键： `C-c & C-n`   
    创建新的snippet模板<sup><a id="fnr.1" class="footref" href="#fn.1">1</a></sup>
-   `M-x yas-visit-snippet-file` 快捷键： `C-c & C-v`   
    查看模板<sup><a id="fnr.2" class="footref" href="#fn.2">2</a></sup>


<a id="orgaf0fd5f"></a>

## snippet 文件内容

    # contributor: pluskid <pluskid@gmail.com>
    # name: __...__
    # --

# Footnotes

<sup><a id="fn.1" href="#fnr.1">1</a></sup> 这里是脚注。。。

<sup><a id="fn.2" href="#fnr.2">2</a></sup> 脚注二。。。
