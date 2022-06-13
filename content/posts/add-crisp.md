---
title: 给文章添加Crisp反馈系统
date: 2019-02-19T16:56:00+08:00
updated: 2019-02-19T16:56:00+08:00
categories: ["toss"]
images: ["images/og/add-crisp.png"]
---

## Chinese ver.
Crisp是一家来自法国的在线反馈服务提供商，因为我用的是 next 主题，所以注册之后直接把邮件的代码粘贴到`~/hexo/themes/next/layout/_custom/head.swig`，其余的设置都可以进入Crisp的后台进行更改。做到了开盖即用。<!--more-->

* 自带微软翻译，虽然很蠢就是了。
* 链接到社交账号，但除了邮箱和手机，其他的好像都404了。
* 提供Android和iOS API。
* 比较完善的团队协作。
* 已读标识
* 介绍页上的几个创始人一直在线，直接面对开发者
* 基本上全是英文

但由于Crisp会挡住我的菜单，所以放弃。如果想要看看效果的话请前往[Crisp官网](https://crisp.chat)点击右下的圆形图标，通常来说，它会加载的比网页要慢一点。

至于我为什么要写这篇文章，当然是因为py过了啊(´ . .̫ . `)

![chat-Crisp-Antoine-screenshot](/images/add-crisp/antoine-chat-crisp.webp)

But my website has no traffic ,and I delete your code and app,sorry Antoine.

## English ver.

Where to post your code depends on what theme you use, but in most time you can post the code in `~/hexo/themes/YOUR-THEME/layout/_partial/head.ejs` or `~/hexo/themes/YOUR-THEME/layout/_custom/head.swig`,if your Hexo theme use different framework,just find the`head.**`file in `layout` folder.

see more at [Crisp Helpdesk](https://help.crisp.chat)

## 后记

其实外国人还是很有趣的嘛，今日任务完成٩(๑´0`๑)۶。
