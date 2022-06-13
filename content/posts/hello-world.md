---
title: 在手机上搭建 hexo 博客
date: 2018-11-11T07:00:00+08:00
updated: 2018-12-16T15:00:00+08:00
categories: ["toss"]
images: ["images/og/hello-world.png"]
---

## 前言

经历了[jimdo](https://jimdo.com)，手打[GitHub](https://github.io)和[WordPress](https://cn.wordpress.org/)之后，终于还是换上了[hexo](https://hexo.io/zh-cn/)，可以看出来博客有着正在向着轻量化发展的趋势，不过随之而来的，是搭建博客所需的基础更高了，虽然各家（指 WordPress 和 hexo）都有自己的开发文档可以帮助你在什么都不懂的情况下快速入门，但不可否认的是，门槛确实在不停地提高。

当然也有[Bitcorn](https://www.bitcron.com/)这样只用设置一次就 OK 的替代品，不过人家在内测，而且我也没有电脑，遂放弃，继续我的 hexo 之旅。

随着手机性能的不断提升，手机编程成为了可能，在此之前，我的 jimdo，GitHub 和 WordPress 都是在手机上完成的，~~虽然这并不算编程~~，不过我一直都在致力于提升 ~~姿势~~ 知识水平，希望能开发出新的技能，在一番误打误撞之后，发现了[Termux](https://termux.com/)。

<!--more-->

## Termux

目前对我来说只有一个作用：hexo，虽说应该算做是大材小用了，不过对于一个起步非常晚的高中生来说，还是写好自己的 hexo 就 ok。

Termux 对我来说就是一个 Linux 模拟器，当然也有其他的终端可供选择，不过由于 Termux 入门，所以对 Termux 有着天生的好感。

## 代码如诗

### 换国内源

首先是喜闻乐见的换国内源环节，当然你也可以选择不换。

```
vi  $PREFIX/etc/apt/sources.list
```

按`i`进入编辑模式，把`https://termux.net`替换为`http://mirrors.tuna.tsinghua.edu.cn/termux`（国内清华源）。

编辑完成后，按住`音量加`点击`E`模拟 `Esc` 键，输入`ZZ`保存并退出，当然也可以直接右滑后长按`KEYBOARD`调出辅助键盘。

### 添加 vim 编辑器中的中文显示支持

```
vim .vimrc
#新建.vimrc 文件并进行编辑
```

粘贴以下内容

```
set fileencodings=utf-8,gb2312,gb18030,gbk,ucs-bom,cp936,latin1
set enc=utf8
set fencs=utf8,gbk,gb2312,gb18030
```

　　编辑完成后，按住`音量加`点击`E`模拟 Ees 键，输入`ZZ`保存并退出，当然也可以直接右滑后长按`KEYBOARD`调出辅助键盘。

```
source .vimrc
#source 变量
```

完成

### 安装 hexo

按顺序执行以下命令。


```
pkg update
#升级包

pkg install vim git nodejs openssh
#询问之后输入 y 然后回车

npm install -g hexo-cli
#安装 hexo

hexo init hexo
#新建一个名为 hexo 的文件夹并初始化 hexo

cd hexo
#进入 hexo 文件夹

npm install
#部署 hexo
```

至此，hexo 已安装完成，指定的文件夹目录如下。

```
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
```

更多信息可以查看[建站|hexo](https://hexo.io/zh-cn/docs/setup)。

继续我们的 hexo。

```
hexo new postname
#postname 就是文章名称

vim source/_posts/postname.md
#用 vim 编辑器编辑 mark down 文本，就是你的文章
```

同上，按`i`进入编辑模式。

编辑完成后，按住`音量加`点击`E`模拟 Ees 键，输入`ZZ`保存并退出，当然也可以直接右滑后长按`KEYBOARD`调出辅助键盘。

```
hexo generate
#生成静态文件

hexo server
#启动服务器
```

以上命令也可以简写为

```
hexo g
hexo s
```

在浏览器输入`http://localhost:4000`即可看到你的网站。至此，hexo 搭建完成。

输入`CTRL`+`c`退出

### 发布到 GitHub & 设置 ssh

本来不想的，结果还是一堆图片，以下是一份超详细的`GitHub`注册教程。

首先需要注册一个 GitHub 账号，地址[https://github.com](https://github.com)。

![github 的 signup](/images/hello-world/01.webp)

点击`Sign up for GitHub`。

![GitHub 注册信息](/images/hello-world/02.webp)

填写自己的信息，用户名，邮箱和密码，出现红色的三角/字，就是用不了的意思，需要换一个别的。

![GitHub 注册确认](/images/hello-world/03.webp)

点击`Create an account`。

![GitHub 费用选择](/images/hello-world/04.webp)

选择白嫖套餐：)。

![确认选择](/images/hello-world/05.webp)

点击`Continue`。

**然后去邮箱点击GitHub发来的连接以完成注册**

![GitHub 页面](/images/hello-world/06.webp)

点击`Desktop version`。

![GitHub 点击+号](/images/hello-world/07.webp)

点击`+`号。

![点击 New repository](/images/hello-world/08.webp)

点击`New repository`。

![GitHub new](/images/hello-world/09.webp)

在`repository name`中填写 username.github.io 。其中，username 是你的用户名，填好后点击`Create repository`然后发现这个↓

![repository](/images/hello-world/10.webp)

点击这个![复制按钮:radio_button:](/images/hello-world/11.webp)

或者复制这个按钮前面的一长串内容。你会得到这样一串字符

```
git@github.com:username/username.github.io.git
```

然后

```
cd hexo
#进入 hexo 文件夹

vim _config.yml
#修改配置文件
```

把 depoly 部分修改为：

```
deploy:
  type: git
  repo: git@github.com:username/username.github.io.git
  branch: master
```
保存并退出

其实就是上面复制的内容，当然你也可以直接填写 repo 部分，username 替换为你的用户名。

回到浏览器

点击`README`新建一个 README 文件用来激活仓库。

![new README](/images/hello-world/12.webp)

随便写一些什么，反正一会就没有了，然后点击`Commit new file`。

![edit README](/images/hello-world/13.webp)

然后你会看见这个：

![edited README](/images/hello-world/14.webp)

点击上方的`settings`进入仓库设置。

![GitHub Settings](/images/hello-world/15.webp)

向下滑找到`GitHub Pages`。

![GitHub Pages setting](/images/hello-world/16.webp)

点击`none`，然后选择`master branch`。

![branch setting](/images/hello-world/17.webp)

点击`save`。

![save branch](/images/hello-world/18.webp)

至此，GitHub端工作完成。

配置 git：

打开Termux，键入：

```
git config --global user.name "Your Name"

git config --global user.email "email@example.com"
#为设备注册姓名与邮箱。
```

```
ssh-keygen -t rsa -C "example@mail.com"
#创建SSH key，引号内替换成你注册GitHub时填的邮箱。
```

之后会要求输入一次文件名，两次密码，可以直接回车忽略，SSH key创建成功之后，运行：

```
vim .ssh/id_rsa.pub
#进入SSH key的文件
```

复制里面所有内容后打开GitHub，点击头像↓

![头像 点击](/images/hello-world/19.webp)

点击`Settings`。

![Settings 点击](/images/hello-world/20.webp)

点击`SSH and GPG keys`。

![Settings](/images/hello-world/21.webp)

点击`new SSH key`。

![keys](/images/hello-world/22.webp)

出现以下内容：

![add SSH key](/images/hello-world/23.webp)

Title填自己喜欢的，Key里面粘贴刚才复制的密匙，填好后点`Add SSH key`

打开Termux，输入：

```
ssh -T git@github.com
#校验SSH key
```

向你确认，输入`yes`后回车。

成功后会显示`Hi rd-dafuz！....`。

然后：

```
npm install hexo-deployer-git --save
#安装git的拓展插件
```

此处报错时常见的解决方案

```
npm config set registry https://registry.npm.taobao.org
#切换到国内的淘宝源，对，阿里巴巴的那个淘宝！
```

### 开始push

```
hexo generate
#生成文件

hexo deploy
#部署文件
```

也可以简写为：

```
hexo g
hexo d
```

或

```
hexo g -d
```

最后出现 INFO Deploy done：git 即为成功,打开 username.github.io 即可查看你的 hexo 了。

## 参考

[Termux 高级终端安装使用配置教程 | 国光](https://www.sqlsec.com/2018/05/termux.html)

[文档 | Hexo](https://hexo.io/zh-cn/docs/)

及百度、bing，请善用搜索引擎。