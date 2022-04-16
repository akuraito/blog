---
title: Hugo PaperMod 初探，相对路径与绝对路径
date: 2021-06-30T18:00:00+08:00
updated: 2021-06-30T18:00:00+08:00
---

今年5月左右把博客从 Hexo-Next 换到了 Hugo PaperMod，告别了大而全，迎来了小而美，尽管没有了侧栏、版权提示、完善的中文支持等，但 Hugo 的生成速度和 PaperMod 的美观度足以弥补这些不足。<!--more-->

本来一切都很不错，直到 Google Analytics 报了一个奇怪的死链：[404gle.cn/box/license.html](https://404gle.cn/box/license.html)。此页内容在迁移主题的过程中移动到了：[404gle.cn/about/](https://404gle.cn/about/)，原 `/box/` 文件夹也全部删去，虽然能正常显示 404 信息，但却缺失了 css 样式表。

经过查看，此问题只出现在二层文件夹的路由中，原因是在引用样式表文件时使用了不完善的相对路径导致了此错误。只需修复相对路径即可，但为了主题文件的完整性，可直接把 `sitedir/themes/PaperMod/layouts/404.html`  复制到 `sitedir/layouts/404.html` 并增加 `<link rel="stylesheet" href="{{ "assets/css/stylesheet.css" | relURL }}">` 即可。（此问题已被修复）

此外，虽然 Hugo 提供了 `relativeurls` （相对路径）选项，但 PaperMod 和大部分 Hugo 主题一样并没有遵守相关语法，导致在建立镜像站点时仅能显示主页，所有可点击项目都是绝对路径，无法通过除输入链接之外的方式访问镜像站点。为了解决这个问题，之前使用的本地生成并上传仓库的工作流需要改为通过 git 同步远端仓库再由自动化软件生成静态页面，并把生成指令设置为 `hugo -b "https://example.com"` 即可分别部署不同镜像。