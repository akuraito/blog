---
title: 我如何设置一台 PC
date: 2021-10-07 17:00:00
updated: 2021-10-07 17:00:00
draft: true
categories: 折腾
---

> 在这个大家一起升 Windows 11 的日子，我选择了进 β 通道！不愧是我.webp :triangular_flag_on_post:<!--more-->
>
> 最大的区别自然是任务栏，只能放在下方，但我觉得迟早会有有方法把它改回去。然后文件管理器默认可以显示 WSL 里面的文件了，巨大进步，对于 WSA 的期待则更进一步。
>
> ![WSL-folder-in-file-manager](../../images/set-a-pc/wsl-folder-in-file-manager.webp)
>
> 是音效！我加了开机音效！打开一个四世同堂的设置后就可以关掉！此外其他音效也有更新。
>
> ![disable-Windows-boot-sound](../../images/set-a-pc/disable-Windows-boot-sound.webp)
>
> 切换桌面时壁纸会有一个从拉伸快速变换的过程，原因见图
>
> ![unload-wallpaper](../../images/set-a-pc/unload-wallpaper.webp)
>
> 输入法也变得纤细了不少。
>
> 小部件是真的没什么用，在开始按钮的微软待办磁贴无法使用之后，这是我对小部件唯一的期待，然而：
>
> ![MS-to-do-widget-broken](../../images/set-a-pc/ms-to-do-widget-broken.webp)
>
> 革命尚未成功，微软仍需努力。
>
> 至于为什么没有 Android 12，和 Windows 一样，有的早就有了，没有就是没有，亲儿子也没有。

然而就在几小时的造作之后，它炸了…

包括任务栏，设置在内的大部分可显示界面失效，由于刚升级就把 Windows.old 给删了所以无法无痛回归，可恶。只能靠着快捷键 <kbd><kbd>Windows</kbd> + <kbd>2</kbd></kbd> 打开浏览器下载 21H1 。

一顿操作之后，正准备打开 office.com 安装三件套，突然一惊，我的 Edge, ALL CLEAR‽

收藏夹，集锦和最重要的密码，全没了。在这万念俱灰的时刻，只有 MS Authenticator 向我伸出了它的双手；只有在这个瞬间，我才明白了它存在的真正意义。~~还好有你！微软！~~

## 所以这是一篇给自己的安装指南与备份

开机第一件事，打开设置/系统/存储，把新文件位置改成 D 盘（为下次 boom 做准备），登上 OneDrive 同步文件，摸出 geek uninstaller 把 Xbox 之流统统删掉，打开 MS store 更新软件，正好也试试 Office Tool Plus，E5 订阅用户请选择企业应用版（Microsoft 365 Apps for enterprise）。

### 浏览器

收藏夹从头再来，密码还算活着，但是拓展全没了，还好在坚果云里找到了今年 4 月的 Tampermonkey 备份，姑且能用吧，倒是 uBlock Origin 只能重来，另外 `https://static.zhihu.com/heifetz/main.signflow.*.js` 由于更名无法使用，请更换为 `https://static.zhihu.com/heifetz/column.signflow.*.js`

由于是最近改的所以还有点印象，打开 `edge://flags/#edge-automatic-https` 即可，see you https everywhere.

### WSL

作为 Windows 的第二生命，WSL 已经是整个生态链中不可或缺的功能，打开设置/应用和功能/程序和功能/启用或关闭 Windows 功能/适用于 Linux 的 Windows 子系统 即可。

重启后开始造作，换镜像，更新，升级，装一堆软件包，顺便学习一下基于 WSL 的 Aria2。

至于其他，都是细枝末节。

### 软件

唯一需要折腾的是 PotPlayer 但我之前是按照 [vcb-s.com/archives/7228](https://vcb-s.com/archives/7228) 来设置的，只好作罢。

## 软件列表

### Microsoft Store

* HyPlayer，等之后换成 LyricEase

* Quicklook，记得装插件

* Windows Terminal

* Ubuntu

* Telegram Desktop

* 微信 For Windows

* QQ桌面版

### others

最早是按照 [Awesome-Windows](https://github.com/Awesome-Windows/Awesome) 来操作的，但毕竟过去那么久了，这次还是选自己熟悉的装。

* geek uninstaller
* Peazip
* PotPlayer，默认也能用
* Typora
* VS Code
* 纯纯写作，只用来同步手机文章
* 华为电脑管家，装了才能控制电池充电

如果不是被逼着用 ie 想要一个 Chrome OS 本。