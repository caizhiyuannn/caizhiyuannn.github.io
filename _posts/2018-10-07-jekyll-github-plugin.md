---
title: Jekyll Plugin
date: 2018-10-07 22:30
categories: jekyll
tags: github jekyll 2018
---

# 在 GitHub 配置 Jekyll 插件

[查看Github Help](https://help.github.com/articles/configuring-jekyll-plugins/)

你可以通过 _config.yml 里面添加插件来拓展额外的功能。

例如：

```yml
plugins:
   - jekyll-mentions
   - jemoji
   - jekyll-redirect-from
   - jekyll-sitemap
   - jekyll-feed
```

## Github 中默认启用的插件，无法进行禁用

```yml
plugins:
    - jekyll-coffeescript
    - jekyll-gist
    - jekyll-github-metadata
    - jekyll-paginate
    - jekyll-relative-links
    - jekyll-optional-front-matter
    - jekyll-readme-index
    - jekyll-default-layout
    - jekyll-titles-from-headings
```

## Github 中可选的插件

```yml
    - jekyll-feed
    - jekyll-redirect-from
    - jekyll-seo-tag
    - jekyll-sitemap
    - jekyll-avatar
    - jemoji
    - jekyll-mentions
    - jekyll-include-cache
```