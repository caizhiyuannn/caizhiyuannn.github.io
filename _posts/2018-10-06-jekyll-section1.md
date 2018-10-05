---
layout: default
title: "使用 jekyll 部署静态站点"
---

# 使用 jekyll 部署静态站点

资源参考： http://jekyll.bootcss.com

## 简介

1. jekyll 是一个博客动态生成静态站点的工具。 不支持动态数据
2. jekyll 不需要数据库，但是可以配合第三方服务
3. jekyll 可以免费部署在GitHub服务器上，天然集成该功能

## jekyll 安装

1. 安装ruby 且版本不能低于2.0
2. 安装rubygems
3. 安装jekyll 用于支持本地预览功能
    - 配置国内 gems 源： gem sources -a https://gems.ruby-china.com/
    - 更新软件（可选）： gem update –system
    - 安装jekyll： gem install jekyll
4. 异常
    - 如运行报错 Missing dependency: rdiscount 则安装 rdiscount

## 快速指南

1. 生成模板
    ```shell
    jekyll new myblog
    cd myblog
    jekyll server
    ```