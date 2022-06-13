---
title: 自由且开放的评论系统 Waline
date: 2021-07-07T18:00:00+08:00
updated: 2021-07-07T18:00:00+08:00
images: ["images/og/achievement-story/waline.png"]
---

自从上手静态博客之后，评论系统就是一个老大难的问题，评论的性质就决定了它需要与用户、数据库交互，提供此功能的第三方服务例如畅言、来必力、Disqus等也并不是那么可靠。除了 Disqus 之外其他服务都几近荒废，自建的评论服务势在必行。<!--more-->

最开始使用的是 Valine[^1]但 Valine 在前台明文显示密匙、邮箱，后期不开放源代码并添加审计等问题，一直忍受到第一次大规模攻击之后，换到了 Waline[^2]。

Waline 可以继承 Valine 的数据库，基于旧版本的 Valine 并添加了基于 serverless 服务器的支持，拥有更好的安全性，并且还在不断更新中。相较于 Valine，Waline 原生支持了评论通知并支持多种通知方式、增加了账号系统并能够强制登录使用、可部署在多种数据库之上还有评论管理、过滤，满足了大部分需求。

由于 Valine 和 Waline 都有官方 next 插件，所以切换还算简单，更换到 Hugo PaperMod 之后则更简便，只需一股脑塞进文件即可[^3]，在使用过程中发现的两个 bug 被公子高速解决，关于前端的问题也多有劳烦  hope 同学。同时公子在博客编译时把评论编译进页面内而不用网页打开之后再加载的方式也很喜欢，只是 Hugo 和 hook 还不甚了解，只能等待日后再进行修改。

[^1]:https://valine.js.org/
[^2]:https://waline.js.org/
[^3]:https://github.com/akuraito/blog/blob/main/layouts/partials/comments.html
