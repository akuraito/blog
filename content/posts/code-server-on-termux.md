---
title: 在 Termux 上使用 code-server
date: 2023-09-04T23:18:00+08:00
updated: 2023-09-04T23:18:00+08:00
categories: ["toss"]
images: ["images/og/code-server-on-termux.png"]
---

每年炸电脑好几次，导致自己培养了一手绝佳的 Windows 重装技巧，尽管如此，每次重装系统仍是一项浩大的工程，首先就是与微软斗智斗勇，然后是与各种广告、同步系统缠斗，但最复杂的，莫过于每次 WSL 环境的搭建，每次都累个半死。思来想去倒是手机常年被毒瘤占据，万万不可重装，不如就把这些东西塞到手机里，好不美哉。

<!--more-->

不同于 ssh，[code-server](https://coder.com/docs/code-server/latest) 提供了基于 web 界面的 VS Code，只需一个现代浏览器便可随意访问，这样一来，桌面端连最基本的软件都不用安装，可谓是完美符合我的需求。当然也可以使用 VS Code 直接连接，但那不在本文的讨论范围。

## 安装

### Termux

目前可从 [F-Droid](https://f-droid.org/en/packages/com.termux) 或 [Github](https://github.com/termux/termux-app/releases) 获取 Termux 安装包，不同来源的 Termux 本体和插件不可通用并且仅推荐从 F-Droid 获取。安装 Termux 之后，请使用以下命令打开图形界面并按需切换镜像以获得更快的访问速度。

```
termux-change-repo
```

然后升级一下有的没的，再安装自己要的工具就行。虽然一直没咋动 Termux，但基础的工具还留着，本文跳过这一部分，请根据报错或手册自行安装。

### code-server

直接按照[官方文档](https://coder.com/docs/code-server/latest/termux#install)运行以下命令即可安装并运行 code-server，**安装时请保证必要的网络条件**。

```
pkg install tur-repo

pkg install code-server

code-server
```

第一次运行 code-server 时会在 `~/.config/code-server/config.yaml` 生成如下配置文件。

```
bind-addr: <ip>:<port>
auth: password
password: <password>
cert: false
```

ip 设为 `0.0.0.0` 便于局域网内访问，选个喜欢的端口和密码之后再次运行`code-server`，即可在浏览器地址栏输入 `<手机的 IP 地址>:<端口>` 打开 code-server。*Termux 查 ip 怪麻烦的？所以直接打开手机设置里的 WiFi 详情查看本机的局域网地址即可。*

![登录界面](/images/code-server-on-termux/code-server-login.webp)

Termux 上的 code-server [无法安装部分插件](https://coder.com/docs/code-server/latest/termux#many-extensions-including-language-packs-fail-to-install)，其中包括了 VS Code 的简体中文语言包，解决方法也很简单（**注意**：使用此方法安装的 code-server 在安装语言包时请选择对应的版本。请依次点击左上的三条横线、Help、About 查看 `Code` 版本）：

1. 下载对应版本的[适用于 VS Code 的中文（简体）语言包](https://open-vsx.org/extension/MS-CEINTL/vscode-language-pack-zh-hans)至电脑
1. 打开拓展（Extensions）界面 / Ctrl+Shift+X
1. 点击展开右上角 `View and More Actions` 的三个圆点并选择 `Install from VSIX`
1. 在弹出的窗口中选择最右侧的 `Show Local`
1. 在弹出的窗口中选择最右侧的 `Open Files`
1. 选择之前下载的文件并重启即可

## Hugo

code-server 安装好之后自然是要，折腾博客！曾几何时，在 Termux 上使用 Hugo 还得[折腾一大堆东西](../hugo-on-termux/)，而现在只需要一行命令即可安装，时代在进步.webp

```
pkg install hugo
```

Hugo 的使用可以查看 [Hugo 快速开始文档](https://gohugo.io/getting-started/quick-start/)，在配置好主题之后，自然要试一试：

```
hugo server
```

然而我们却看到输出的信息显示：`Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)`

点击这个链接后，会打开形如 `http://192.168.0.42:8081/proxy/1313/` 的网址，Hugo 和 PaperMod 可不知道 `/proxy/1313/` 是什么意思，只会告诉你，css 和图片找不到啦！于是只好使用以下命令，把网址设置为手机的局域网地址并使局域网内可以访问，顺带解决根路径导致的素材丢失问题。

```
hugo server -b http://192.168.0.42/ --bind="0.0.0.0"
```

在 code-server 中，Markdown 文件的预览暂时不可用，也只好开着 `hugo server` 来预览了。

![hugo server 预览](/images/code-server-on-termux/hugo-server.webp)

## 图片

然而，就在一切就绪时，Open Graph 里的图片应该从哪里来成为了问题。作为一个坚定的 *PowerPoint 是世界上最方便实用的制图软件*拥护者，之前的图基本上都是 Powerpoint 做出来的，然而每次安装 office 也很麻烦，Windows 自带的画图成为了仅剩的选择。事实上，不少网页编辑器和新媒体工具的使用方法基本上就是 PowerPoint 同款操作，在素材足够的情况下绘画这一步骤可以省略，自己用形状拼图形也足以胜任大部分的工作；相对画图有着更多的可调整项，相对 Photoshop 更加轻量，可惜为了 All in Browser 的美好愿景必须被抛弃。总之，先用画图凑合着吧。（绘图时画图还未添加图层功能）

![old og image for code-server on termux](/images/code-server-on-termux/code-server-on-termux-old.webp)

画图在添加图层功能之后方便了很多，但对于精细到像素的对齐依旧只能依靠鼠标所在的像素点来心算、保存的文件也无法包含图层信息。而 Web 端的类 PowerPoint 编辑器通常都面临着字体和版权的不便，思来想去，Web 端的设计工具便只有——Figma！想来是符合这一堆需求的，大不了用 css 写也行。

-----

自己摸索了下 Figma， 网页端使用本地字体需要安装插件且需要开机启动，直接照之前的模板进行一个复刻。可惜插件终究得舍弃，还得找找下一个替代品。

![og image for code-server on termux](/images/code-server-on-termux/code-server-on-termux.webp)