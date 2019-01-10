---
title: "Emacs use-package 包"
date: <span class="timestamp-wrapper"><span class="timestamp">&lt;2018-10-15 Mon 00:50&gt;</span></span>
layout: post
categories: 
tags: 
---

# Table of Contents

1.  [Emacs 第三方包 use-package](#org3f73040)
    1.  [安装 use-package](#org7937e21)
        1.  [开始](#org739a9a3)
    2.  [按键绑定 Key-binding](#org279d4e3)
    3.  [](#orgcb94f24)


<a id="org3f73040"></a>

# Emacs 第三方包 use-package

Use-package 是一个宏, 它能让你将一个包的 require 和它的相关的初始化等配置组织 在一起, 避免对同一个包的配置代码散落在不同的文件中.


<a id="org7937e21"></a>

## 安装 use-package

1.  通过GitHub克隆源码进行安装
2.  通过 MELPA 包仓库进行安装


<a id="org739a9a3"></a>

### 开始

简单的声明 use-package 的例子

{% highlight emacs-lisp %}
;; This is only needed once, near the top of the file
(eval-when-compile
  ;; Following line is not needed if use-package.el is in ~/.emacs.d
  (add-to-list 'load-path "<path where use-package is installed>")
  (require 'use-package))

(use-package foo)
{% endhighlight %}

-   (use-package foo) 会引入foo包，只有在它可用的时候。如果不可用，则通过buffer `*Messages*` 进行告警
-   使用 `:init` 关键字在包加载前执行需要的指令，它接受一个或多个参数，直到下一个关键字的出现
    
    {% highlight emacs-lisp %}
    (use-package foo
      :init
      (setq foo-variable t))
    {% endhighlight %}
-   类似的， `:config` 关键字在包加载后执行需要的指令，在懒加载的情况（autoloads），会推迟到自动加载之后。可以和 `:init` 一起使用
    
    {% highlight emacs-lisp %}
    (use-package foo
      :init
      (setq foo-variable t)
      :config
      (foo-mode 1))
    {% endhighlight %}
-   通过 `:commands`  关键字可以生成autoload方式进行加载， `:bind` 关键字来绑定按键， `:map` 指定map模式来绑定
    
    {% highlight emacs-lisp %}
    (use-package color-moccur
      :commands (isearch-moccur isearch-all)
      :bind (("M-s O" . moccur)
             :map isearch-mode-map
             ("M-o" . isearch-moccur)
             ("M-O" . isearch-moccur-all))
      :init
      (setq isearch-lazy-highlight t)
      :config
      (use-package moccur-edit))
    {% endhighlight %}


<a id="org279d4e3"></a>

## 按键绑定 Key-binding

-   加载模块时一般会绑定按键
    
    {% highlight emacs-lisp %}
    (use-package ace-jump-mode
      :bind ("C-." . ace-jump-mode))
    {% endhighlight %}

-   `:bind` 主要做两件事情：
    
    > 1.  为ace-jump-mode 创建自动加载(autoload)，推迟加载指定需要使用的时候。
    > 2.  为ace-jump-mode 绑定按键 C-. 可以通过 M-x describe-personal-keybindings 来查看所有的按键绑定

-   下面例子与上面行为一直：
    
    {% highlight emacs-lisp %}
    (use-package ace-jump-mode
      :commands ace-jump-mode
      :init
      (bind-key "C-." 'ace-jump-mode))
    {% endhighlight %}


<a id="orgcb94f24"></a>

## 
