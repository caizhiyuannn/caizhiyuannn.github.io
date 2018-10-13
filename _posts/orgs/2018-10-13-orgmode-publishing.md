---
title: "Org Mode 发布文档"
date: <span class="timestamp-wrapper"><span class="timestamp">&lt;2018-10-13 Sat&gt;</span></span>
layout: post
categories: 
- emacs
tags: 
- orgmode 
- emacs 
- linux 
- lisp
---

# Table of Contents

1.  [Publishing](#org4850473)
2.  [发布文档需要通过配置文件实现](#orge961b01)
    1.  [Project alist (alist 是一个类似dict一样的数据类型，可以存储键值)](#org2187699)
    2.  [指定源和目标](#org79a17da)
    3.  [选择文件（用于识别需要发布的文件）](#org952b1ac)
    4.  [发布触发执行动作](#org0b1b916)
    5.  [发布可选项](#orga537272)
        1.  [通用属性](#org07243e6)
        2.  [ASCII 指定属性](#org3af0b45)
        3.  [Beamer 指定属性](#org84d2d59)
        4.  [HTML 指定属性](#org94e993c)
        5.  [LaTeX 指定属性](#org828d4c1)
        6.  [Markdown 指定属性](#orgbb06c37)
        7.  [ODT 指定属性](#orga58c020)
        8.  [Texinfo 指定属性](#orgf0d579c)
        9.  [一个复杂的例子](#org6d250df)
    6.  [Sitemap](#org8b89858)
    7.  [跨页面索引](#orgd1c2bcd)


<a id="org4850473"></a>

# Publishing

Org 有一个发布管理系统，允许你将项目的文件自动转化成HTML，可以自动导出对应的css，js，image等文件部署到web服务器。
也可以将org 转化成markdown， pdf 等格式


<a id="orge961b01"></a>

# 发布文档需要通过配置文件实现


<a id="org2187699"></a>

## Project alist (alist 是一个类似dict一样的数据类型，可以存储键值)

-   变量 org-publish-project-alist
    
    配置文件几乎都是通过 org-publish-project-alist 变量的设置来实现，每个项目有两种方式进行配置
    
    1.  ("project-name" :property value :property value &#x2026;)
    
    2.  ("project-name" :components ("project-name" "project-name" &#x2026;))
        
        通过 components 可以将多个 project-name 绑定，达到一次转化多个项目文件，例如html，css，image通过三个project-name设置，
        这是通过components 绑定三个project-name ，发布时只需要指定一个项目名


<a id="org79a17da"></a>

## 指定源和目标

一般配置 org-publish-project-alist 有许多可选项，但是一定要指定 源 和 目标 位置才能正确识别要发布的文件或项目文件夹

-   **:base-directory**
    指定包含源文件的目录，即需要发布文件的基本目录

-   **:publishing-directory**
    指定转化后存放的目录

-   **:preparation-function**
    指定转化文件前需要调用的函数， 例如发布前需要 make 一下源文件

-   **:completion-function**
    指定转化文件完成后需要调用的函数


<a id="org952b1ac"></a>

## 选择文件（用于识别需要发布的文件）

一般默认扩展名为 **.org** 的认为是项目文件，可以通过以下属性改变

-   **:base-extension**
    指定识别的文件拓展名， **不需要点(.)后缀** ，如：\*:base-extension "css"\*
-   **:exclude**
    用于排除指定文件
-   **:include**
    引入指定文件，存在该文件都会进行发布转化
-   **:recursive**
    为真时， 将递归检查发布 base-directory 指定目录下的文件


<a id="org0b1b916"></a>

## 发布触发执行动作

发布在将源目录文件复制到目标目录文件并可能进行相关转化，默认 org 文件转化成 HTML ，它是通过调用 HTML export 的 org-html-publish-to-html 函数转化。

你也可以使用 org-latex-publish-to-pdf 或者 ascii, Texinfo, 等等来完成相应的功能。。

其它像image 图像文件这样只需要将源目录文件复制到目标目录，则可以调用 **org-publish-attachment** 来完成复制操作

如果需要转化非 org 文件，或 org 文件通过转化成其它文件，可以指定发布调用的函数：

-   **:publishing-function**
    执行发布操作将触发指定函数来完成工作
-   **:htmlized-source**
    如果为 **真** ， 则发布的文件将是 html 风格的文件，具有html标签


<a id="orga537272"></a>

## 发布可选项

org-publish-project-alist 可以配置额外的选项增加支持

注意： 如果文件内部添加 export 设置， 将会覆盖这些对应配置。


<a id="org07243e6"></a>

### 通用属性

    :archived-trees                         org-export-with-archived-trees
    :exclude-tags	                        org-export-exclude-tags
    :headline-levels	                org-export-headline-levels
    :language	                        org-export-default-language
    :preserve-breaks	                org-export-preserve-breaks
    :section-numbers	                org-export-with-section-numbers
    :select-tags	                        org-export-select-tags
    :with-author	                        org-export-with-author
    :with-broken-links	                org-export-with-broken-links
    :with-clocks	                        org-export-with-clocks
    :with-creator	                        org-export-with-creator
    :with-date	                        org-export-with-date
    :with-drawers	                        org-export-with-drawers
    :with-email	                        org-export-with-email
    :with-emphasize	                        org-export-with-emphasize
    :with-fixed-width	                org-export-with-fixed-width
    :with-footnotes	                        org-export-with-footnotes
    :with-latex	                        org-export-with-latex
    :with-planning	                        org-export-with-planning
    :with-priority	                        org-export-with-priority
    :with-properties                        org-export-with-properties
    :with-special-strings	                org-export-with-special-strings
    :with-sub-superscript	                org-export-with-sub-superscripts
    :with-tables	                        org-export-with-tables
    :with-tags	                        org-export-with-tags
    :with-tasks	                        org-export-with-tasks
    :with-timestamps	                org-export-with-timestamps
    :with-title	                        org-export-with-title
    :with-toc	                        org-export-with-toc
    :with-todo-keywords	                org-export-with-todo-keywords


<a id="org3af0b45"></a>

### ASCII 指定属性

    :ascii-bullets                          org-ascii-bullets
    :ascii-caption-above	                org-ascii-caption-above
    :ascii-charset	                        org-ascii-charset
    :ascii-global-margin	                org-ascii-global-margin
    :ascii-format-drawer-function	        org-ascii-format-drawer-function
    :ascii-format-inlinetask-function	org-ascii-format-inlinetask-function
    :ascii-headline-spacing	                org-ascii-headline-spacing
    :ascii-indented-line-width	        org-ascii-indented-line-width
    :ascii-inlinetask-width	                org-ascii-inlinetask-width
    :ascii-inner-margin	                org-ascii-inner-margin
    :ascii-links-to-notes	                org-ascii-links-to-notes
    :ascii-list-margin	                org-ascii-list-margin
    :ascii-paragraph-spacing	        org-ascii-paragraph-spacing
    :ascii-quote-margin	                org-ascii-quote-margin
    :ascii-table-keep-all-vertical-lines	org-ascii-table-keep-all-vertical-lines
    :ascii-table-use-ascii-art	        org-ascii-table-use-ascii-art
    :ascii-table-widen-columns	        org-ascii-table-widen-columns
    :ascii-text-width	                org-ascii-text-width
    :ascii-underline	                org-ascii-underline
    :ascii-verbatim-format	                org-ascii-verbatim-format


<a id="org84d2d59"></a>

### Beamer 指定属性

    :beamer-theme                           org-beamer-theme
    :beamer-column-view-format	        org-beamer-column-view-format
    :beamer-environments-extra	        org-beamer-environments-extra
    :beamer-frame-default-options	        org-beamer-frame-default-options
    :beamer-outline-frame-options	        org-beamer-outline-frame-options
    :beamer-outline-frame-title	        org-beamer-outline-frame-title
    :beamer-subtitle-format	                org-beamer-subtitle-format


<a id="org94e993c"></a>

### HTML 指定属性

    :html-allow-name-attribute-in-anchors           org-html-allow-name-attribute-in-anchors
    :html-checkbox-type	                        org-html-checkbox-type
    :html-container	                                org-html-container-element
    :html-divs	                                org-html-divs
    :html-doctype	                                org-html-doctype
    :html-extension	                                org-html-extension
    :html-footnote-format	                        org-html-footnote-format
    :html-footnote-separator	                org-html-footnote-separator
    :html-footnotes-section	                        org-html-footnotes-section
    :html-format-drawer-function	                org-html-format-drawer-function
    :html-format-headline-function	                org-html-format-headline-function
    :html-format-inlinetask-function	        org-html-format-inlinetask-function
    :html-head-extra	                        org-html-head-extra
    :html-head-include-default-style	        org-html-head-include-default-style
    :html-head-include-scripts	                org-html-head-include-scripts
    :html-head	                                org-html-head
    :html-home/up-format	                        org-html-home/up-format
    :html-html5-fancy	                        org-html-html5-fancy
    :html-indent	                                org-html-indent
    :html-infojs-options	                        org-html-infojs-options
    :html-infojs-template	                        org-html-infojs-template
    :html-inline-image-rules	                org-html-inline-image-rules
    :html-inline-images	                        org-html-inline-images
    :html-link-home	                                org-html-link-home
    :html-link-org-files-as-html	                org-html-link-org-files-as-html
    :html-link-up	                                org-html-link-up
    :html-link-use-abs-url	                        org-html-link-use-abs-url
    :html-mathjax-options	                        org-html-mathjax-options
    :html-mathjax-template	                        org-html-mathjax-template
    :html-metadata-timestamp-format	                org-html-metadata-timestamp-format
    :html-postamble-format	                        org-html-postamble-format
    :html-postamble	                                org-html-postamble
    :html-preamble-format	                        org-html-preamble-format
    :html-preamble	                                org-html-preamble
    :html-table-align-individual-fields	        org-html-table-align-individual-fields
    :html-table-attributes	                        org-html-table-default-attributes
    :html-table-caption-above	                org-html-table-caption-above
    :html-table-data-tags	                        org-html-table-data-tags
    :html-table-header-tags	                        org-html-table-header-tags
    :html-table-row-tags	                        org-html-table-row-tags
    :html-table-use-header-tags-for-first-column	org-html-table-use-header-tags-for-first-column
    :html-tag-class-prefix	                        org-html-tag-class-prefix
    :html-text-markup-alist	                        org-html-text-markup-alist
    :html-todo-kwd-class-prefix	                org-html-todo-kwd-class-prefix
    :html-toplevel-hlevel	                        org-html-toplevel-hlevel
    :html-use-infojs	                        org-html-use-infojs
    :html-validation-link	                        org-html-validation-link
    :html-viewport	                                org-html-viewport
    :html-xml-declaration	                        org-html-xml-declaration
    :body-only                                      ;; only export section between <body></body>


<a id="org828d4c1"></a>

### LaTeX 指定属性

    :latex-active-timestamp-format          org-latex-active-timestamp-format
    :latex-caption-above	                org-latex-caption-above
    :latex-classes	                        org-latex-classes
    :latex-class	                        org-latex-default-class
    :latex-compiler	                        org-latex-compiler
    :latex-default-figure-position	        org-latex-default-figure-position
    :latex-default-table-environment	org-latex-default-table-environment
    :latex-default-table-mode	        org-latex-default-table-mode
    :latex-diary-timestamp-format	        org-latex-diary-timestamp-format
    :latex-footnote-defined-format	        org-latex-footnote-defined-format
    :latex-footnote-separator	        org-latex-footnote-separator
    :latex-format-drawer-function	        org-latex-format-drawer-function
    :latex-format-headline-function	        org-latex-format-headline-function
    :latex-format-inlinetask-function	org-latex-format-inlinetask-function
    :latex-hyperref-template	        org-latex-hyperref-template
    :latex-image-default-height	        org-latex-image-default-height
    :latex-image-default-option	        org-latex-image-default-option
    :latex-image-default-width	        org-latex-image-default-width
    :latex-images-centered	                org-latex-images-centered
    :latex-inactive-timestamp-format	org-latex-inactive-timestamp-format
    :latex-inline-image-rules	        org-latex-inline-image-rules
    :latex-link-with-unknown-path-format	org-latex-link-with-unknown-path-format
    :latex-listings-langs	                org-latex-listings-langs
    :latex-listings-options	                org-latex-listings-options
    :latex-listings	                        org-latex-listings
    :latex-minted-langs                     org-latex-minted-langs
    :latex-minted-options	                org-latex-minted-options
    :latex-prefer-user-labels	        org-latex-prefer-user-labels
    :latex-subtitle-format	                org-latex-subtitle-format
    :latex-subtitle-separate	        org-latex-subtitle-separate
    :latex-table-scientific-notation	org-latex-table-scientific-notation
    :latex-tables-booktabs	                org-latex-tables-booktabs
    :latex-tables-centered	                org-latex-tables-centered
    :latex-text-markup-alist	        org-latex-text-markup-alist
    :latex-title-command	                org-latex-title-command
    :latex-toc-command	                org-latex-toc-command


<a id="orgbb06c37"></a>

### Markdown 指定属性

    :md-footnote-format	org-md-footnote-format
    :md-footnotes-section	org-md-footnotes-section
    :md-headline-style	org-md-headline-style


<a id="orga58c020"></a>

### ODT 指定属性

    :odt-content-template-file	org-odt-content-template-file
    :odt-display-outline-level	org-odt-display-outline-level
    :odt-fontify-srcblocks	        org-odt-fontify-srcblocks
    :odt-format-drawer-function	org-odt-format-drawer-function
    :odt-format-headline-function	org-odt-format-headline-function
    :odt-format-inlinetask-function	org-odt-format-inlinetask-function
    :odt-inline-formula-rules	org-odt-inline-formula-rules
    :odt-inline-image-rules	        org-odt-inline-image-rules
    :odt-pixels-per-inch	        org-odt-pixels-per-inch
    :odt-styles-file	        org-odt-styles-file
    :odt-table-styles	        org-odt-table-styles
    :odt-use-date-fields	        org-odt-use-date-fields


<a id="orgf0d579c"></a>

### Texinfo 指定属性

    :texinfo-active-timestamp-format	org-texinfo-active-timestamp-format
    :texinfo-classes	                org-texinfo-classes
    :texinfo-class	                        org-texinfo-default-class
    :texinfo-table-default-markup	        org-texinfo-table-default-markup
    :texinfo-diary-timestamp-format	        org-texinfo-diary-timestamp-format
    :texinfo-filename	                org-texinfo-filename
    :texinfo-format-drawer-function	        org-texinfo-format-drawer-function
    :texinfo-format-headline-function	org-texinfo-format-headline-function
    :texinfo-format-inlinetask-function	org-texinfo-format-inlinetask-function
    :texinfo-inactive-timestamp-format	org-texinfo-inactive-timestamp-format
    :texinfo-link-with-unknown-path-format	org-texinfo-link-with-unknown-path-format
    :texinfo-node-description-column	org-texinfo-node-description-column
    :texinfo-table-scientific-notation	org-texinfo-table-scientific-notation
    :texinfo-tables-verbatim	        org-texinfo-tables-verbatim
    :texinfo-text-markup-alist	        org-texinfo-text-markup-alist


<a id="org6d250df"></a>

### 一个复杂的例子

{% highlight elisp %}
(setq org-publish-project-alist
      '(("orgfiles"
         :base-directory "~/org/"
         :base-extension "org"
         :publishing-directory "/ssh:user@host:~/html/notebook/"
         :publishing-function org-html-publish-to-html
         :exclude "PrivatePage.org"   ;; regexp
         :headline-levels 3
         :section-numbers nil
         :with-toc nil
         :html-head "<link rel=\"stylesheet\"
                  href=\"../other/mystyle.css\" type=\"text/css\"/>"
         :html-preamble t)

        ("images"
         :base-directory "~/images/"
         :base-extension "jpg\\|gif\\|png"
         :publishing-directory "/ssh:user@host:~/html/images/"
         :publishing-function org-publish-attachment)

        ("other"
         :base-directory "~/other/"
         :base-extension "css\\|el"
         :publishing-directory "/ssh:user@host:~/html/other/"
         :publishing-function org-publish-attachment)
        ("website" :components ("orgfiles" "images" "other"))))
{% endhighlight %}


<a id="org8b89858"></a>

## TODO Sitemap


<a id="orgd1c2bcd"></a>

## 跨页面索引

org-mode 可以通过一个发布的项目文件生成页面索引，

-   **:makeindex**
    当值为 **真** ，将会生成 theindex.org 并发布为 theindex.html

-   设置 **:makeindex**, 项目第一次发布是索引文件会被创建，该文件只包含 **#+INCLUDE: "theindex.inc"** 声明。
    
    你可以在这个声明文件中添加标题，样式等。
    
    索引条目通过 **#+INDEX** 关键字指定，包含感叹号的条目将创建子项
    
        * Curriculum Vitae
        #+INDEX: CV
        #+INDEX: Application!CV
