---
title: "EMACS 发送邮件"
date: <span class="timestamp-wrapper"><span class="timestamp">&lt;2018-10-19 Fri 03:23&gt;</span></span>
layout: post
categories: 
- emacs
tags: 
- emacs 
- send\_email
---

# Table of Contents

1.  [基础](#org4cedf84)
    1.  [快捷键](#org8869a9e)
2.  [邮件消息格式](#org569410a)
3.  [标准邮件头字段信息](#org8d1a3a6)
4.  [别名或分组邮件地址](#orgfda9a56)
5.  [编辑邮件的特殊命令](#org05be796)
    1.  [引用邮件](#orgad29396)
    2.  [其它](#org19c70d2)
6.  [添加签名](#org4c9c656)
7.  [Amuse](#org28d45cd)
8.  [Methods](#orge6ae3fc)


<a id="org4cedf84"></a>

# 基础

emacs 要发送邮件，通过 `C-x m` 切换到新的缓冲区新建邮件，完成后，通过 `C-c C-s` 或 `C-c C-c` 完成发送。   
**参考** ：[GNU 官方手册](https://www.gnu.org/software/emacs/manual/html_node/emacs/Sending-Mail.html)


<a id="org8869a9e"></a>

## 快捷键

|---|---|
| 快捷键 | 用途 |
|---|---|
| `C-x m` | 创建新的邮件 |
|---|---|
| `C-x 4 m` | 在其他窗口新建邮件 |
|---|---|
| `C-x 5 m` | 在一个新的frame中新建邮件 |
|---|---|
| `C-c C-s` | 在邮件buffer中发送邮件 |
|---|---|
| `C-c C-c` | 在邮件buffer中发送邮件，完成后关闭buffer |
|---|---|


<a id="org569410a"></a>

# 邮件消息格式

示例

    To: subotai@example.org
    Cc: mongol.soldier@example.net, rms@gnu.org
    Subject: Re: What is best in life?
    From: conan@example.org
    --text follows this line--
    To crush you enemies, see them driven before you, and to
    hear the lamentation of their women

| 格式 | 说明 |
|---|---|
| `To` | 收件人 |
|---|---|
| `Cc` | 抄送人 |
|---|---|
| `Bcc` | 密送人 |
|---|---|
| `From` | 发件人 |
|---|---|
| `Subject` | 标题 |
|---|---|


<a id="org8d1a3a6"></a>

# 标准邮件头字段信息

你可以使用任何头字段信息，但是正常情况下只接受标准头字段信息

-   `From`
    1.  可以使用存地址格式： `king@grassland.com`
    2.  使用地址和全名格式： `'king@grassland.com (Elvis Parsley)'`
    3.  另一种格式： `'Elvis Parsley <king@grassland.com>'`
-   `To`
    收件人
-   `Subject`
    标题
-   `CC`
    抄送人
-   `BCC`
    密送人
-   `FCC`
    文件名，附加已发送邮件的副本
-   `Reply-to`
    回复人地址， 如果每种原因通过 `From` 发件人无法收到回复，可以使用选项
-   配置默认头
    
    {% highlight emacs-lisp %}
    (setq mail-default-headers
          "Reply-to: foo@example.com")
    {% endhighlight %}


<a id="orgfda9a56"></a>

# 别名或分组邮件地址

你可以定义邮件人别名，默认邮件人别名定义文件为 `~/.mailrc` ，你可以通过变量 `mail-personal-alias-file` 指定其它的文件来保存别名。   
格式如下：

    # alias nick fulladdress
    
    alias maingnu gnu@gnu.org local-gun
    alias jsmith "John Q. Smith <none@example.com>"
    source ~/mail_alias

-   `nick`   
    表示别名
-   `fulladdress`
    表示邮件地址，可以是单个地址，也可以是多个空格分割的地址，
-   可以引入其它设置的别名文件


<a id="org05be796"></a>

# 编辑邮件的特殊命令

| 快捷键 | 用途 | 命令 |
|---|---|---|
| `C-c C-f C-t` | 移动到To头部 | `(message-goto-to)` |
|---|---|---|
| `C-c C-f C-s` | 移动到Subject | `(message-goto-subject)` |
|---|---|---|
| `C-c C-f C-c` | 移动到CC | `(message-goto-cc)` |
|---|---|---|
| `C-c C-f  C-b` | 移动到BCC | `(message-goto-bcc)` |
|---|---|---|
| `C-c C-f C-r` | 移动到Reply-to | `(message-goto-reply-to)` |
|---|---|---|
| `C-c C-f C-f` | 移动到Mail-Followup-To | `(message-goto-followup-to)` |
|---|---|---|
| `C-c C-b` | 移动到正文 | `(message-goto-fcc)` |
|---|---|---|


<a id="orgad29396"></a>

## 引用邮件

-   `C-c C-y`
    从邮件阅读器中取出选定的邮件作为引用需要回复的邮件
-   `C-c C-q`
    填充引用消息的段落，


<a id="org19c70d2"></a>

## 其它

| 命令或快捷键 | 用途 |
|---|---|
| `C-c C-a` | 添加附件 |
|---|---|
| `M-x ispell-message` | 正文进行拼写检查，会跳过引用的邮件 |
|---|---|
| hooks | `C-x m` 会触发 `text-mode-hook`, `message-mode-hook` |
|---|---|


<a id="org4c9c656"></a>

# 添加签名

变量 `message-signature` 可以定义邮件签名，或者可以直接从邮件正文加入签名。

默认变量 `message-signature`  为 `t`, 它会自动解析 `~/.signature` 文件记录的签名信息并插入邮件中。

可以通过变量 `message-signature-file` 指定其它的文件来保存签名。

如果变量 `message-signature` 不为真，可以通过 `C-c C-w(message-insert-signature)` 来写入签名。


<a id="org28d45cd"></a>

# TODO Amuse


<a id="orge6ae3fc"></a>

# TODO Methods
