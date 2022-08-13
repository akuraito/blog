---
title: C-Lodop 排错
date: 2022-08-02T17:00:00+22:00
updated: 2022-08-02T17:00:00+22:00
categories: ["toss"]
images: ["images/og/clodop-without-https.png"]
---

## 缘起

今天同学想打印一份成绩证明，结果试来试去都是`CLodop云打印服务(localhost本地)未安装启动!`之前逛教务处网站的时候也看到过这个提示，因为要安装软件且短时间内没有需求，就一直搁置，没想到居然还是个坏的。<!--more-->

## 上手

既然有报错那肯定就直接复制搜索一气呵成，可惜不管怎么搜都是同一个结果出现千百遍，对遇到的情况没帮助不说，来源还不可考，也不知道是谁抄谁。

![搜索结果](../../images/clodop-without-https/bing-search.webp)

尝试捷径失败，还是只能自己动手，兜兜转转回到了教务处的网站上来。打开控制台一看，这不是写的清清楚楚的嘛，早知道这样，何必那么麻烦。

![报错](../../images/clodop-without-https/ensure-private-network-requests-are-made-from-secure-contexts.webp)

谷歌已经在 [Chrome 开发者博客](https://developer.chrome.com/blog/private-network-access-update/) 写清楚啦，没 https 就不要乱动！如果我就是要乱动，那也不是不行，只需要打开浏览器里的实验功能，并把 `Block insecure private network requests` 设为关闭就好啦，也可以在地址栏输入 `chrome://flags/#block-insecure-private-network-requests` 直达此选项。（Edge 浏览器也可直接输入，并将自动跳转到 `edge://flags/#block-insecure-private-network-requests`）

如果同学是电脑小白也没有问题，直接让他/她打开学校的远程接入系统（WebVPN）即可，此网页配置了 https 且代理了校内大部分网站，一定程度上可以绕过跨域问题。