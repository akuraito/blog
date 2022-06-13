---
title: Hugo 初探，theme-akura
date: 2021-07-12T18:00:00+08:00
updated: 2021-07-12T18:00:00+08:00
images: ["images/og/achievement-story/hugo-theme-akura.png"]
---

Hugo 看了半天，也没有几个好看又好用的主题，毕竟 go 更多的在后端使用，即使是目前在用的 PaperMod 也有不少不如人意的地方，但好在 Hugo 简单的语法让自己设计一套主题成为可能。<!--more-->

## Hugo 语法

Hugo 基于 go 语言，模板则使用了 `html/template` 和 `text/template` ，在使用时用 `{{ 双大括号 }}` 包裹。作为大部分语言的核心，变量和函数起主要作用，而在模板的编写方面也继承了 go 语言的特色：`if` 嵌套 `if` 。

首先要编写的文件位于 `layouts/_default/baseof.html` ，这是 Hugo 渲染的默认模板，设置了网页的结构，首先使用 `{{- partial "head.html" .}}` 引入 `<head>` 部分文件，同理引入顶栏、侧栏、文章部分页面。除了有显示文章的页面，还另需页面用以显示文章目录，这就引出了页面类型：`single page` 和 `list page` ，利用 `list page` 即可构造目录，此外还有归档、标签、分类、站点地图、RSS等页面需要分别编写模板。

如果想要完善主题，便可在 `theme.toml` 中添加配置项，例如：当配置中出现了 `disableScrollToTop: true` 则不渲染下方被 `if` 包裹的内容。

```
{{- if (not .Site.Params.disableScrollToTop) }}

{{- end }}
```

## HTML 与 CSS

因为并没有详细的构建过大型项目，所以目前还处于按图索骥的环节，自然也不妄想使用现代的网站框架，只用最基础的HTML 与 CSS 来构造网页，除了评论系统需要交互外不启用 JS 。

## PaperMod 重构

大体上保持 PaperMod 的外观效果，主页更改为类 [og.png](https://404gle.cn/images/og.png) 或者 [GitHub 仓库社交预览图](https://opengraph.githubassets.com/200a992730df60f592c31f8de7f19379ed60bda3016706ac2b4273fe879631a1/akuraito/blog) 的样式，深色模式使用且只使用 `prefers-color-scheme` ：

```
<link rel="stylesheet" href="main.css">
<link rel="stylesheet" href="dark.css" media="(prefers-color-scheme: dark)">
```

链接不使用下划线而使用 `::after` 和 `:focus` 构造，评论框透明，评论样式跟随主题样式。

