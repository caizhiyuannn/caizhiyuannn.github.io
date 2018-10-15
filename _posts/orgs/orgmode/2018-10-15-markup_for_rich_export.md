---
title: "org-mode 丰富导出内容标记"
date: <span class="timestamp-wrapper"><span class="timestamp">&lt;2018-10-15 Mon 00:10&gt;</span></span>
layout: post
categories: 
- emacs
tags: 
- emacs 
- orgmode
---

# Table of Contents

1.  [简介](#orgca08222)
2.  [段落](#org91c18e4)
3.  [强调和等宽字体](#org406c3fe)
4.  [水平线规则](#org3f244d5)
5.  [图像和表格](#org7640e2c)
6.  [Literal examples](#org783b3e5)
7.  [特殊符号](#org4d429f7)
8.  [上标和下标](#org8617668)
9.  [在org文档中嵌入 LaTeX](#org310b962)


<a id="orgca08222"></a>

# 简介

[官网文档链接](https://orgmode.org/manual/Markup.html#Markup)   
由于像HTML、LaTeX 允许更丰富的格式，org-mode 也提供标记用于丰富导出的格式。


<a id="org91c18e4"></a>

# 段落

段落之间至少有一行空行分割来表示换行，如果需要在段落中加强断行符，可以行尾添加"\\\\"。

-   为了在一个区域中保留换行符、缩进和空白行，但是在其他情况下使用普通格式，可以使用一下格式，
    
        快捷键： <v TAB
        
        #+BEGIN_VERSE
         Great clouds overhead
         Tiny black birds rise and fall
         Snow covers Emacs
        
             -- AlexSchroeder
        #+END_VERSE

-   当引用另一份文件的段落时，习惯上把它格式化为在左页边和右页边缩进的段落。你可以在Org模式的文档中包括这样的引用:
    
        快捷键：<q TAB
        
        #+BEGIN_QUOTE
        Everything should be made as simple as possible,
        but not any simpler -- Albert Einstein
        #+END_QUOTE

-   如果要居中文字，可以这样引用：
    
        快捷键： <c TAB
        
        #+BEGIN_CENTER
        Everything should be made as simple as possible, \\
        but not any simpler
        #+END_CENTER


<a id="org406c3fe"></a>

# 强调和等宽字体

|---|---|
| 格式 | 用法 |
|---|---|
| **粗体** | `*粗体*` |
|---|---|
| *斜体* | `/斜体/` |
|---|---|
| <span class="underline">下划线</span> | `_下划线_` |
|---|---|
| `原样输出` | `=保持原样输出，内部字符会显示=` |
|---|---|
| `代码` | `~代码~` |
|---|---|
| <del>strike-through</del> | `+这里是删除线+` |
|---|---|

-   [ ] 其它, 待翻译
    
    > To turn off fontification for marked up text, you can set org-fontify-emphasized-text to nil.
    > To narrow down the list of available markup syntax, you can customize org-emphasis-alist.
    > To fine tune what characters are allowed before and after the markup characters,
    > you can tweak org-emphasis-regexp-components.
    > Beware that changing one of the above variables will not take effect until you reload Org,
    > for which you may need to restart Emacs.


<a id="org3f244d5"></a>

# 水平线规则

只有破折号至少五个的一行将会以水平线导出，如： `-----`

---


<a id="org7640e2c"></a>

# TODO 图像和表格


<a id="org783b3e5"></a>

# Literal examples

-   主要用于示例展示，格式内容将会原样输出。
    
        格式：<e TAB
        
        #+BEGIN_EXAMPLE
        Some example from a text file.
        #+END_EXAMPLE

-   代码块展示
    
        指定编程语言将支持高亮
        
        #+BEGIN_SRC emacs-lisp
          (defun org-xor (a b)
             "Exclusive or."
             (if a (not b) b))
        #+END_SRC


<a id="org4d429f7"></a>

# 特殊符号

可以使用 LaTeX-like 风格的语法插入特殊符号，例如 `\alpha` 表示希腊字母， `\to` 表示箭头。
如果在单词中需要这样一个符号，那么用一对花括号结束它。
例如：

> Pro tip: Given a circle `\Gamma` of diameter d, the length of its circumference
> is `\pi{}d`.
> 
> Pro tip: Given a circle &Gamma; of diameter d, the length of its circumference
> is &pi;d.

-   `C-c C-x \` 显示 UTF8 字符，将显示LaTeX风格特殊字符的显示效果


<a id="org8617668"></a>

# TODO 上标和下标


<a id="org310b962"></a>

# TODO 在org文档中嵌入 LaTeX
