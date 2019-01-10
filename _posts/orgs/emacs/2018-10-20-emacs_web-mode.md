---
title: "Emacs Web-Mode 包手册"
date: <span class="timestamp-wrapper"><span class="timestamp">&lt;2018-10-20 Sat 00:02&gt;</span></span>
layout: post
categories: 
- emacs
tags: 
- emacs 
- web-mode 
- package
---

# Table of Contents

1.  [简介](#org13b3efe)
    1.  [功能特色](#org701defc)
2.  [安装](#org2e966a4)
    1.  [源码使用](#orgbacf58f)
    2.  [关联引擎](#org534b431)
3.  [自定义](#org64b80b8)
    1.  [缩进](#orgb6770a9)
    2.  [开启和关闭功能](#org9cfb0ec)
4.  [快捷键](#org7f8318b)
    1.  [一般](#org86b3b7b)
    2.  [DOM](#orgd5f44af)
    3.  [块](#org9b95449)
    4.  [HTML元素](#orga8e3dd8)
    5.  [HTML标记](#org1055c2d)
    6.  [HTML属性](#org149f35f)


<a id="org13b3efe"></a>

# 简介

web-mode.el 是 emacs 的一个用于编辑 web 模板的主模式。

模板引擎兼容：php, jsp, gsp (grails), asp / asp.net ajax (atlas), 
django / twig / jinja(2) / erlydtl (zotonic) / selmer, erb, ejs, 
freemarker, velocity, cheetah, smarty, ctemplate / mustache / hapax / handlebars / meteor / blaze / ember.js / velvet, 
blade (laravel), knockoutjs, go template (revel), razor/play, dust, closure (soy), underscore.js, template-toolkit, 
liquid (jekyll), angular.js, web2py, mako (pylons), reactjs (jsx), mojolicious, elixir (erlang), thymeleaf, cl-emb, 
heist, archibus, xoops, hero, spip

[web-mode官网文档](http://web-mode.org/)


<a id="org701defc"></a>

## 功能特色

-   自动缩进
-   开闭标记之间跳转， `C-c C-n`
-   dom 导航，
-   代码折叠， `C-c C-f`
-   HTML 标签自动关闭 `(<div></ → <div>|</div>)` ，自动打开 `(<div>RET</div> → (<div>\n··|\n</div>)` ，
    自动展开 `(d/s/ → <div><span>|</span></div>)` ，属性自动引用 `( style= → style="|")`
-   语法高亮
-   snippet片段插入 `C-c C-s`
-   符号自动配对
-   注释和取消注释 `M-:`
-   智能选择和拓展 `C-c C-m`
-   css 颜色显示
-   空白检测 `C-c C-w`
-   等等..


<a id="org2e966a4"></a>

# 安装

[官网下载链接](https://raw.github.com/fxbois/web-mode/master/web-mode.el)


<a id="orgbacf58f"></a>

## 源码使用

源码使用需要加载路径到 `load-path` ，用 `package.el` 安装 `package-initialize` 后无需调用 `(require 'web-mode)`

{% highlight emacs-lisp %}
(require 'web-mode)
(add-to-list 'auto-mode-alist '("\\.phtml\\'" . web-mode))
(add-to-list 'auto-mode-alist '("\\.tpl\\.php\\'" . web-mode))
(add-to-list 'auto-mode-alist '("\\.[agj]sp\\'" . web-mode))
(add-to-list 'auto-mode-alist '("\\.as[cp]x\\'" . web-mode))
(add-to-list 'auto-mode-alist '("\\.erb\\'" . web-mode))
(add-to-list 'auto-mode-alist '("\\.mustache\\'" . web-mode))
(add-to-list 'auto-mode-alist '("\\.djhtml\\'" . web-mode))
;; 编辑html纯文件可以通过下面语句默认生效web-mode
(add-to-list 'auto-mode-alist '("\\.html?\\'" . web-mode))
{% endhighlight %}


<a id="org534b431"></a>

## 关联引擎

如果一个文件的拓展名是未知的，可以强制关联指定的处理引擎

{% highlight emacs-lisp %}
(setq web-mode-engines-alist
      '(("php"    . "\\.phtml\\'")
        ("blade"  . "\\.blade\\.")))
{% endhighlight %}


<a id="org64b80b8"></a>

# 自定义

可以通过hook来添加自定义的设置

{% highlight emacs-lisp %}
(defun my-web-mode-hook ()
  "Hooks for Web mode."
  (setq web-mode-markup-indent-offset 2))
(add-hook 'web-mode-hook  'my-web-mode-hook)
{% endhighlight %}


<a id="orgb6770a9"></a>

## 缩进

{% highlight emacs-lisp %}
;; HTML元素缩进偏移
(setq web-mode-markup-indent-offset 2)

;; CSS缩进偏移
(setq web-mode-css-indent-offset 2)

;; Script/code offset indentation (for JavaScript, Java, PHP, Ruby, Go, VBScript, Python, etc.)
(setq web-mode-code-indent-offset 2)

;; You can disable arguments|concatenation|calls lineup with
(add-to-list 'web-mode-indentation-params '("lineup-args" . nil))
(add-to-list 'web-mode-indentation-params '("lineup-calls" . nil))
(add-to-list 'web-mode-indentation-params '("lineup-concats" . nil))
(add-to-list 'web-mode-indentation-params '("lineup-ternary" . nil))
{% endhighlight %}

默认情况下，标签属性是这样缩进的：

{% highlight html %}
<img src="pix.png"
     class="noborder"/>
{% endhighlight %}

你可以通过 `web-mode-attr-indent-offset` 强制固定缩进

{% highlight html %}
<img src="pix.png"
  class="noborder"/>
{% endhighlight %}


<a id="org9cfb0ec"></a>

## 开启和关闭功能

{% highlight emacs-lisp %}
;; 自动配对
(setq web-mode-enable-auto-pairing t)

;; CSS 着色
(setq web-mode-enable-css-colorization t)

;;Block face: can be used to set blocks background and default foreground (see web-mode-block-face)
(setq web-mode-enable-block-face t)

;; Part face: can be used to set parts background and default foreground (see web-mode-script-face and web-mode-style-face which inheritate from web-mode-part-face)
(setq web-mode-enable-part-face t)

;; Comment keywords (see web-mode-comment-keyword-face)
(setq web-mode-enable-comment-interpolation t)

;; Heredoc (cf. PHP strings) fontification (when the identifier is <<<EOTHTML or <<<EOTJAVASCRIPT)
(setq web-mode-enable-heredoc-fontification t)
{% endhighlight %}


<a id="org7f8318b"></a>

# 快捷键


<a id="org86b3b7b"></a>

## 一般

| 快捷键 | 说明 |
|---|---|
| `M-;` | 注释/取消注释行 |
|---|---|
| `C-c C-f` | 折叠标签或者块 |
|---|---|
| `C-c C-i` | 缩进整个buffer |
|---|---|
| `C-c C-m` | 标记或者拓展 |
|---|---|
| `C-c C-s` | 插入snippet |
|---|---|
| `C-c C-w` | 显示无效空格 |
|---|---|


<a id="orgd5f44af"></a>

## DOM

| 快捷键 | 说明 |
|---|---|
| `C-c C-d a` | 替换撇号 |
|---|---|
| `C-c C-d d` | 显示不匹配标签 |
|---|---|
| `C-c C-d e` | 替换HTML条目 |
|---|---|
| `C-c C-d n` | 正常化 |
|---|---|
| `C-c C-d q` | replace dumb quotes |
|---|---|
| `C-c C-d t` | 跨越dom树 |
|---|---|
| `C-c C-d x` | xpath |
|---|---|


<a id="org9b95449"></a>

## 块

| 快捷键 | 说明 |
|---|---|
| `C-c C-b b` | 块开始 |
|---|---|
| `C-c C-b c` | 块关闭 |
|---|---|
| `C-c C-b e` | 块结束 |
|---|---|
| `C-c C-b k` | 删除块 |
|---|---|
| `C-c C-b n` | 下一个块 |
|---|---|
| `C-c C-b p` | 上一个块 |
|---|---|
| `C-c C-b s` | 块选择 |
|---|---|


<a id="orga8e3dd8"></a>

## HTML元素

| 快捷键 | 说明 |
|---|---|
| `C-c C-e /` | 元素关闭 |
|---|---|
| `C-c C-e a` | 选择元素内容 |
|---|---|
| `C-c C-e b` | 元素开始 |
|---|---|
| `C-c C-e c` | 元素克隆 |
|---|---|
| `C-c C-e d` | 子元素 |
|---|---|
| `C-c C-e e` | 元素结束 |
|---|---|
| `C-c C-e f` | 折叠子元素 |
|---|---|
| `C-c C-e i` | 元素插入 |
|---|---|
| `C-c C-e k` | 删除元素 |
|---|---|
| `C-c C-e m` | 子元素之间空白 |
|---|---|
| `C-c C-e n` | 下一个元素 |
|---|---|
| `C-c C-e p` | 上一个元素 |
|---|---|
| `C-c C-e r` | 重命名元素 |
|---|---|
| `C-c C-e s` | 选择元素 |
|---|---|
| `C-c C-e t` | 颠倒元素 |
|---|---|
| `C-c C-e u` | 父元素 |
|---|---|
| `C-c C-e v` | 元素消失 |
|---|---|
| `C-c C-e w` | 包装元素 |
|---|---|


<a id="org1055c2d"></a>

## HTML标记

| 快捷键 | 说明 |
|---|---|
| `C-c C-t a` | 排序属性 |
|---|---|
| `C-c C-t b` | 标签的开始 |
|---|---|
| `C-c C-t e` | 标签的结束 |
|---|---|
| `C-c C-t m` | 获取匹配的标签 |
|---|---|
| `C-c C-t n` | 下一个标签 |
|---|---|
| `C-c C-t p` | 上一个标签 |
|---|---|
| `C-c C-t s` | 选择标签 |
|---|---|


<a id="org149f35f"></a>

## HTML属性

| 快捷键 | 说明 |
|---|---|
| `C-c C-a b` | 属性的开始 |
|---|---|
| `C-c C-a e` | 属性的结束 |
|---|---|
| `C-c C-a i` | 插入属性 |
|---|---|
| `C-c C-a k` | 删除属性 |
|---|---|
| `C-c C-a n` | 下一个属性 |
|---|---|
| `C-c C-a p` | 上一个属性 |
|---|---|
| `C-c C-a s` | 选择属性 |
|---|---|
| `C-c C-a t` | 属性颠倒 |
|---|---|
