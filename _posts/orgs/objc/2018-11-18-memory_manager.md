---
title: "IOS 内存管理"
date: <span class="timestamp-wrapper"><span class="timestamp">&lt;2018-11-18 Sun 03:30&gt;</span></span>
layout: post
categories: 
- IOS
tags: 
- memory\_manager
---

# Table of Contents

1.  [需要内存管理](#orge02c732)
2.  [引用计数器](#org05b4f61)
    1.  [对象被销毁的原则](#org3dec1a0)


<a id="orge02c732"></a>

# 需要内存管理

1.  NSObject 所有子类都要进行内存管理
2.  C C++ 进行混合编程时需要进行内存管理
3.  基础数据类型不需要内存管理，如int, bool char类型


<a id="org05b4f61"></a>

# 引用计数器

1.  初始值为0
2.  使用alloc、new、copy 操作，引用计数器将会加1
3.  引用计数器为0 的时候，内存将会释放
4.  retain 标记 引用计数器 +1
5.  release 时候 引用计数器 -1
6.  


<a id="org3dec1a0"></a>

## 对象被销毁的原则

1.  引用计数器为0的时候， 对象被销毁。
2.  对象被销毁使用一般会调用： dealloc方法执行操作
