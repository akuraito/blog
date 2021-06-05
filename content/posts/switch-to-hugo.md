---
title: 切换到 HUGO
date: 2021-05-16T17:13:47+08:00
updated: 2021-05-16T17:13:47+08:00
categories: 折腾
---

生命在于折腾。<!--more-->

在不断的添加各种功能尤其是压缩文件这一耗时大户之后，我的 Hexo 网站生成时间已经到达了惊人的 3.76 s 。正好前几天看到了一款对胃口的HUGO主题 [hugo-PaperMod](https://github.com/adityatelange/hugo-PaperMod) ，rss、sitemap、暗色模式、搜索、还有一直想弄一个的 `profile-mode` ，当即上手整一个:tada:。

## HUGO

HUGO 站点与 Hexo 共存了大半个月，终于还是完全切换到 HUGO ，只用把 `permalink` 改成如下就能完美迁移，只要是在 `posts` 文件夹下的文章都会按照这个格式生成。

```toml
[permalinks]
  posts = "essay/:filename"
```

HUGO 还有个 `hasCJKLanguage` 选项，如果文章中使用了很多中文引号的话可以开启，但标题 `ĀKURAI's` 里的 `'` 每次就只能写成 `&#39;` ，只好关闭。

同时，HUGO 默认转义 Markdown 文件中的 HTML 代码，如需开启的话：

```toml
[markup.goldmark.renderer]
  unsafe = true
```

## Vercel

使用 `git modules` 时 Vercel 只能使用 http 连接而不能使用加密连接。

Vercel 默认的 HUGO 版本过于老旧，需要在 vercel.json 里设置：

```json
{
  "build": {
    "env": {
      "HUGO_VERSION": "0.83.1"
    }
  }
}
```

## GitHub

此次更新顺便还全部把文件备份到了 GitHub ，也算是小小的一次升级吧。

## Cloudflare

由于最近 Vercel 疑似失联，所以套了一个 Cloudflare CDN。

由于和 Vercel 的相性问题，需要关闭 `始终使用 HTTPS` 并在  `/.well-known/*` 上关闭安全性。（这都什么鬼翻译？

对于任何支持手动更改暗色模式功能的网站，请关闭 `Rocket Loader™`。

直接开启 `电子邮件地址混淆技术` 将会降低网站加载速度。