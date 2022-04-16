---
title: 使用Cloud studio制作一个WordPress网站
date: 2018-12-31T08:55:00+08:00
updated: 2018-12-31T08:55:00+08:00
categories: ["artificial"]
---

腾讯和 coding 一起搞了一个东西叫做[Cloud Studio](https://studio.dev.tencent.com),可以用来搭建动态网站，并且准备好了各种环境，简单上手，如果只是搭建一个 WordPress 站点，确实能够完成传说中的 5 分钟快速完成。<!--more-->

<hr>

> 由于 Cloud Studio 已于 2020 年 1 月 30 日停止服务并转换为 Cloud Studio 团队版，本教程将不再适用。

<hr>

## 开始

首先注册一个 [Cloud Studio](https://studio.dev.tencent.com) 账号，需要微信扫码登录，对于只有一个手机的人，请进入[腾讯云](https://cloud.tencent.com)，选择 QQ 或者 邮箱 登陆，之后再打开 Cloud studio ，浏览器会自动调用 cookies 登陆，所以需要在同一个浏览器里进行以上操作。

另外，由于手机 UA 显示不完整，请选择带有 电脑模式/桌面版 等选项的浏览器，如果不知道应该选什么浏览器比较好，遇事不决 [Chrome](https://google.cn/chrome)

![](/images/wordpress-on-cloud-studio/01.webp)

登录后点击进入工作空间。

![](/images/wordpress-on-cloud-studio/02.webp)

点击`新建工作空间`。

![](/images/wordpress-on-cloud-studio/03.webp)

来源选择`腾讯云开发者平台`。

![](/images/wordpress-on-cloud-studio/04.webp)

填写`项目名`。

选择`从模板创建`。

选择 `WordPress` 模板。

点击`创建`。

![](/images/wordpress-on-cloud-studio/05.webp)

点击进入你刚才创建的工作空间。

![](/images/wordpress-on-cloud-studio/06.webp)

界面如下：

![](/images/wordpress-on-cloud-studio/07.webp)

点击浏览器的电脑模式。

![](/images/wordpress-on-cloud-studio/08.webp)

点击右侧的`一键部署`。

![](/images/wordpress-on-cloud-studio/09.webp)

点击`一键开启`。

![](/images/wordpress-on-cloud-studio/10.webp)

点击`一键部署`按钮。

![](/images/wordpress-on-cloud-studio/11.webp)

点击`测试域名`即可看见你的 `WordPress` 站点。

![](/images/wordpress-on-cloud-studio/12.webp)

点击 `Let's go!` 会要求你输入`数据库名`、`用户名`、`密码`和`数据库主机地址`。

所以，点击上方的`资源管理`。

![](/images/wordpress-on-cloud-studio/13.webp)

![](/images/wordpress-on-cloud-studio/14.webp)

复制`数据库名`、`用户名`、`密码`和`数据库主机地址`，在 WordPress 中填写完毕后点击 `submit`。

![](/images/wordpress-on-cloud-studio/15.webp)

填写正确之后开始安装 WordPress。

![](/images/wordpress-on-cloud-studio/16.webp)

点击 `Run the installation`。

![](/images/wordpress-on-cloud-studio/17.webp)

设置`网站名称`、`用户名`（不是数据库用户名）、`密码`和你的`邮箱`。

![](/images/wordpress-on-cloud-studio/18.webp)

**不勾选**不被搜索引擎收录，点击 `lnstall` 以安装WordPress。

![](/images/wordpress-on-cloud-studio/19.webp)

告诉你安装成功了，点击 `Log in`。

![](/images/wordpress-on-cloud-studio/20.webp)

输入刚刚设置的用户名和密码，点击 `Log in` 即可看见 WordPress 的仪表盘。

![](/images/wordpress-on-cloud-studio/21.webp)

至此，WordPress 已经搭建完成，但由于 Cloud studio 的特殊性，它不能在设置中设置语言、安装插件/主题，（其实主要是因为连接不上 [wordpress.org](https://wordpress.org)）也不能使用 Akism 的评论过滤，并且数据库容量和磁盘容量都只有 128mb。

## 使用 语言/插件/主题

以安装中文支持为例。

进入 [make.wordpress.org/polyglots/teams/](https://make.wordpress.org/polyglots/teams/)，找到 简体中文 的语言包

![](/images/wordpress-on-cloud-studio/22.webp)

点击 `View Team Page` 进入[下载页面](https://make.wordpress.org/polyglots/teams/?locale=zh_CN)

![](/images/wordpress-on-cloud-studio/23.webp)

点击 `Download language pack`，并在一个文件夹中解压文件。

![](/images/wordpress-on-cloud-studio/24.webp)

![](/images/wordpress-on-cloud-studio/25.webp)

回到 Cloud studio。

![](/images/wordpress-on-cloud-studio/26.webp)

长按 wp-config-sample.php，点击下载并打开文件。

![](/images/wordpress-on-cloud-studio/27.webp)

填写数据库名、数据库用户名、密码和数据库地址。

![](/images/wordpress-on-cloud-studio/28.webp)

在最后一行新增：

```
define ('WPLANG', 'zh_CN');
```

然后复制文件的所有内容。

![](/images/wordpress-on-cloud-studio/29.webp)

回到 Cloud studio 。

点击：`文件` 。

点击：`新建文件`。

![](/images/wordpress-on-cloud-studio/30.webp)

填写以下内容。

```
/wp-config.php
```

![](/images/wordpress-on-cloud-studio/31.webp)

粘贴刚才复制的 .config 文件

![](/images/wordpress-on-cloud-studio/32.webp )

点击：`文件`。

点击：`新建文件夹`。

![](/images/wordpress-on-cloud-studio/33.webp)

输入

`wp-content/languages`

并按回车。

![](/images/wordpress-on-cloud-studio/34.webp)

长按 languages 文件夹。

点击：`上传`。

![](/images/wordpress-on-cloud-studio/35.webp)

选择语言包解压之后的文件并上传。

![](/images/wordpress-on-cloud-studio/36.webp)

上传成功之后是这样的。

![](/images/wordpress-on-cloud-studio/37.webp)

点击：`重新部署`。

![](/images/wordpress-on-cloud-studio/38.webp)

点击 WordPress 的 `sitting/general`。

选择站点语言为：zh_CN。

![](/images/wordpress-on-cloud-studio/39.webp)

点击：`Save Changes`。

![](/images/wordpress-on-cloud-studio/40.webp)

可以看见仪表盘已经变成了中文。

其他的插件也是相同的步骤，不过如果不在意这些插件，语言，确实能够实现5分钟搭建。

~~如果想要绑定自己的域名，按  Coding 官方教程来应该是没什么用的，首先 ping 一下域名，等解析成功之后去 coding 反馈区反馈，大概半天就会在工作人员的帮助下解析到网站了。~~

此问题已修复

## 以及全新的 WordPress 编辑器

![](/images/wordpress-on-cloud-studio/41.webp)

![](/images/wordpress-on-cloud-studio/42.webp)

![](/images/wordpress-on-cloud-studio/43.webp)

![](/images/wordpress-on-cloud-studio/44.webp)

![](/images/wordpress-on-cloud-studio/45.webp)

![](/images/wordpress-on-cloud-studio/46.webp)

　跟 jimdo 一个逻辑，不过比 jimdo 好太多

![](/images/wordpress-on-cloud-studio/47.webp)

![](/images/wordpress-on-cloud-studio/48.webp)

![](/images/wordpress-on-cloud-studio/49.webp)

![](/images/wordpress-on-cloud-studio/50.webp)
