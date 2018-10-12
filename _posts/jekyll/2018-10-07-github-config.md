---
layout: post
title: "jekyll _config.yml in github pages"
date: "2018-10-07 22:00"
---

# 配置 Jekyll

[查看GitHub Help](https://help.github.com/articles/configuring-jekyll/)

GitHub Pages 可以通过 jekyll 部署，可以通过 _config.yml 配置更多的设置

## GitHub 中可以改变的选项

```yml
github: [metadata]
encoding: UTF-8
kramdown:
    input: GFM
    hard_wrap: false
    
future: true
jailed: false
theme: jekyll-theme-primer
gfm_quirks: paragraph_end

```

## GitHub 中不可以改变的选项

```yml
lsi: false
safe: true
source: [your repo's top level directory]
incremental: false
highlighter: rouge
gist:
    noscript: false
kramdown:
    math_engine: mathjax
    syntax_highlighter: rouge
```


## jekyll 文档头信息
Jekyll 要求 Markdown 文件每个文件头需要添加头信息， 头信息只是一些元数据， 通过三个破折号分割

```markdown

---
title: This is title
layout: post
---

```

或者不添加元数据，但是必须要通过三个破折号分割声明

```markdown
---
---
```
