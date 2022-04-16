---
title: 使用 Termux搭建Hugo
date: 2019-05-19T08:00:00+08:00
updated: 2019-05-19T08:00:00+08:00
author: Aral Balkan
post_link: https://ar.al/2018/07/30/web-development-on-a-phone-with-hugo-and-termux/
categories: ["translation"]
---

## 缘起　·　Why

hexo 虽好，但 node 依赖以及生成速度迟早会成为一个问题，虽然现在文章还比较少，没有这方面的烦恼，不过造作总是给人带来欢乐。因为国际信道的原因，简单尝试一番之后并没有成功，只有高考之后再来玩。<!--more-->

以下是我找到的一篇成功范例，就权当作提升英语水平了。

## 正文　·　Text

![Web development in 2018: all you need is a phone.](/images/hugo-on-termux-tslt/instance.webp)

> 设备：S9+，微软可折叠蓝牙键盘
> 编辑器：Emacs
> 浏览器：DuckDuckGo rendered ver.

Hugo 是一个高效、快速的静态站点生成器和网站架构，和其他大部分生成器一样，你可以使用 Termux 在手机上方便的使用 Hugo 来搭建静态网站。

### 食用方式　·　How

（原作者运行环境为 LineageOS 15.1 、 Termux 0.64 以及顺滑的国际网络，以下说明均在此环境中完成。）

1. 安装 [来自于 F-Droid 的 Termux](https://f-droid.org/packages/com.termux/)

2. 在 Termux 中安装 Go （如果你使用 zsh 的话，请把 *.bashrc* 替换成 *.zshrc*）

```zsh
#安装 Go
pkg install golang

#更新 shell 配置
echo "export GOPATH=$HOME/go\nexport PATH=$PATH:$GOROOT/bin:$GOPATH/bin" >> ~/.bashrc

#重新加载 shell 配置
source ~/.bashrc
```

3 编译源代码

```zsh
#安装 Mage（一个 Go 的构建工具）
go get github.com/magefile/mage

#检索，编译以及安装 Hugo
cd ${GOPATH:-$HOME/go}/src/github.com/gohugoio/hugo
env DEPNOLOCK=1 mage vendor
mage install
```

大功告成

现在，你应该已经有了一个可用的 Hugo站点 ,在手机上享受网站开发的快乐。

## 参考　·　Source

原文链接： [Web development on a phone with Hugo and Termux](https://ar.al/2018/07/30/web-development-on-a-phone-with-hugo-and-termux/)


## 关于　·　About

~~本文章采用**cc by-sa**许可协议。~~

Aral Balkan 的网站已更新许可协议为 CC BY-NC-SA 4.0

非利益相关。