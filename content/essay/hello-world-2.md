---
title: Termux and Hexo使用指北？
date: 2019-02-05 17:27:00
updated: 2019-04-05 17:27:00
categories: 折腾
---

## 须知

- 本文全都是为了搭建 Hexo 博客而写，只讲必要的操作/知识/技巧，更加具体的知识请查阅最末的[参考](#参考)。

实践本文需要：

- 一台 Android5.0 以上的手机
- 一定的 Linux 基础
- 实践过上一篇文章 [在手机上搭建 hexo 博客](/essay/hello-world/)
- 一定的英语水平
- 一定的 百度 能力
- 耐心<!--more-->

## Termux

### Termux Code

Termux 简单来说就是一个 Android 上的 Linux 模拟器，最大的作用是 ~~让你回忆起图形界面的友善(ㆁωㆁ*)~~ 把手机当成电脑用，并且官方封装了一堆包，可以快速提升你的英语水平以及相信~~女装加成~~的神秘力量。

把手机当成电脑用，顾名思义， ~~把手机横过来再接上键盘和鼠标之后，你就会拥有一台 Linux 电脑~~ 你会得到一个完全不会产生兴趣的黑色界面，所幸我只用教弄好 Hexo 就完事了。既然它现在是一台电脑，那就一定会和各种各样的文件与文件夹打交道，所以列举一下必要的几种形式。

| 表现形式 | 类型 | 举例 |
| ------ | ------ | ------ |
| * | 文件夹/文件 | hexo/CNAME |
| .* | 隐藏文件夹/文件 | .ssh/.gitignore |
| . | 当前所在文件夹 | . |
| .. | 上一层文件夹 | .. |

在 Windows 和 Mac 中我们可以使用`双击`/`单击`/`右键`对文件进行操作，但在 Termux 里面并没有这么便利。（所有的`↵`标准意味着按一次回车键，大部分的命令都在按下回车键后执行，仅在此处作演示。）

```
ls↵
#展示出当前文件夹中的文件夹/文件

ls hexo↵
#展示出`hexo`文件夹中的文件夹/文件

ls -a↵
#展示出当前文件夹中所有文件夹/文件（包括隐藏）

ls -a hexo↵
#展示出`hexo`文件夹中所有文件夹/文件（包括隐藏）

cd hexo↵
#进入 hexo 文件夹

cd↵
#返回`Termux`的根目录

cd ..↵
#返回上一层文件夹

cd hexo/themes↵
#进入 hexo 的主题文件夹

mkdir hexo↵
#新建一个名为 hexo 的文件夹

vim 1.md↵
#新建/编辑一个名为 1.md 的文件

cp 01.txt 01/01↵
#复制名为 01.txt 的文件到名为 01/01 文件夹

cp -r 01 02↵
#复制名为 01 的文件夹到名为 02 的文件夹
```

作为自带的文件编辑器， vim 设计的初衷是经历减少鼠标的使用，使用方法大概是这样的：

![vim-full-use](/images/hello-world-2/vim-full-use.webp)

相信你也是不会没事用 vim 在屏幕输入设备上打字的人，所以我们需要记住的就只有下面这一张：

![vim-vi-workmodel](/images/hello-world-2/vim-vi-workmodel.webp)

输入 i/a/o 之后复制粘贴保存退出一气呵成，这才是它应有的宿命。

### Termux ohmyzsh

让你的 Termux 变好看/用一点。

项目地址：[Termux-ohmyzsh](https://github.com/Cabbagec/termux-ohmyzsh)

食用方式：

```
sh -c "$(curl -fsSL https://github.com/Cabbagec/termux-ohmyzsh/raw/master/install.sh)"
```

点击确认授权 文件权限 ，之后会要求输入数字选择 配色 和 字体 ，随便选一个就好，更多新奇操作请参见项目主页。

```
Enter a number, leave blank to not to change: 14
Enter a number, leave blank to not to change: 6
```

确认退出后重启生效。

## Hexo

### Hexo code

Hexo 使用中常用的指令：

```
hexo n 1
#新建一篇名为 1 的文章

hexo g
#生成静态文件

hexo g -d
#生成静态文件并部署

hexo s
#启动服务器。默认情况下，访问地址为 http://localhost:4000/

hexo d
#部署网站

hexo clean
#清除缓存文件 (db.json) 和已生成的静态文件 (public)

vim source/_posts/1.md
#编辑名为 1 的文章/名为 1.md 的文件
```

![hexo-build](/images/hello-world-2/hexo-build.webp)

### Front-matter

打开名为 1 文章之后，里面会含有这样的一串字符

![vim-post-edit](/images/hello-world-2/vim-post-edit.webp)

Front-matter 规定了每一篇文章不同于其他文章的变量,比如上图中的字符规定了 文章标题 和 文章建立时间 ，如果需要别的可以新起一行，需要注意的是冒号后面一定要有一个空格。

>|参数|	描述|默认值|
>| ------ | ------ | ------ |
>|layout	|布局||
>|title|标题||
>|date|	建立日期	|文件建立日期|
>|updated	|更新日期|文件更新日期|
>|comments|开启文章的评论功能|	true|
>|tags	|标签（不适用于分页）||
>|categories|分类（不适用于分页）||
>|permalink|覆盖文章网址|||

食用示例

![vim-post-edited](/images/hello-world-2/vim-post-edited.webp)

### Markdown

说完了虚线里面的，来说说虚线下面的。虚线下面的就是你写的文章，所有的文章采用 markdown 进行编写，同时也支持特定的 别名 与 html ，需要注意的是 Markdowm 拥有众多方言，**部分 markdown 需要两个换行符才能实现真正的换行**，使用前请注意当前正在使用的 markdown 是什么版本，接下来讲讲比较通用的 markdown 格式。

#### 标题

和 html 一样， markdown 支持多级标题（一般最多能支持到 6 级），使用标题时请注意 **`#`号与文字之间需要有一个空格，`#`号必须顶格**。标题除了让你的字变得更大之外，还能生成一个一个的文章目录，所以请勿滥用标题。

![文章目录](/images/hello-world-2/toc.webp)

格式

```
# 一级标题
## 二级标题
### 三级标题
################# 很多级标题
```

演示

![purewrite-picshort-markdown-heads](/images/hello-world-2/heads.webp)

#### 加粗

在需要加粗的字符两侧分别打两个`*`号。

```
**我会变得很大**
```

**我会变得很大**

#### 斜体

在需要使用斜体的字符两侧分别打一个`*`号。

```
*啊我斜了*
```

*啊我斜了*

#### 删除线

在需要使用删除线的字符两侧分别打两个`~`号（注意使用英文`~`符号。

```
~~(¯―¯٥)~~
```

~~(¯―¯٥)~~

#### 引用

在字符前输入`>`+`空格`，和标题一样， markdown 也支持多级引用，依然需要中间有一个空格，依然需要顶格。

```
> 一级引用
> > 二级引用
> > > > > > > 很多级引用
```

> 一级引用
> > 二级引用
> >
> > > > > > > 很多级引用

#### 列表

列表分为无序列表和有序列表，无序列表是`*`/`+`/`-`+`空格`+ 文字 组成，有序列表是`数字`+`英文句号`+`空格`+文字组成，需要一提的是无论数字写得是几， Markdowm 都会将它们正确的排列起来。支持嵌套，注意空格。

##### 无序列表

```
- 包子
- 油条
- 稀饭
```

- 包子
- 油条
- 稀饭

##### 有序列表

```
1. 包子
2. 馒头
1. 稀饭
```

1. 包子
2. 馒头
1. 稀饭

##### 列表嵌套

列表使用`tab`键进行嵌套，并支持混合嵌套，多重嵌套。

```
- 早饭
     1. 包子
     2. 馒头
```

- 早饭
     1. 包子
     2. 馒头

#### 代码块

在`markdown`中共有两种代码块，分别是`行内代码`和
```
多行代码。
```

##### 行内代码

在需要使用行内代码的字符两侧分别打一个 ` 号（反引号）。

```
我是一个`行内代码`
```

我是一个`行内代码`

##### 多行代码

分别在需要使用行内代码的前一行和后一行用三个 ` 号(反引号）包起来。

![markdown 多行代码](/images/hello-world-2/code.webp)

```
我是多行代码
```

#### 链接

分别用`[]`包裹需要显示出来的文字，用`()`包裹网页地址，网页地址可以是相对地址也可以是绝对地址。

```
[my blog](https://www.404gle.cn)
```

[my blog](https://www.404gle.cn)

#### 图片

把链接的格式前面加一个`!`（英文感叹号）就是图片的格式。因为使用 Termux 来移动图片实在是不方便，所以请老实的使用图床，比如[SMMS](https://sm.ms)。

```
![head](https://404gle.cn/images/avatar.webp)
```

![head](https://404gle.cn/images/avatar.webp)

#### ~~表格~~

markdown 表格就是个坑，如果想展示表格，请把 excel 文件保存为 html 格式，再复制粘贴到 .md 文件 中

#### 阅读全文(摘要)

大部分 hexo 主题支持在 Markdowm 文件中使用`<!--more-->`进行截断，只需在 Markdowm 文件中合适的位置添加`<!--more-->`，首页（指 index.html）就会显示`<!--more-->`之前的内容与一个`阅读全文`按钮。

![hexo-next-readmore](/images/hello-world-2/hexo-next-readmore.webp)

当然也有部分主题为了美观，只显示文章最前面的固定字数的文字。不过还是建议在写Markdowm文档时就添加一个`<!--more-->`，否则一朝换主题，唯有泪千行。反正也不会乱显示，有备无患总是好的。

#### 总结

除了上面的常规操作之外， markdown 语法之间也可以互相嵌套，比如：~~中国最大`种子`网站~~**上线啦，[点击进入](http://www.zzj.moa.gov.cn/)**

当然 markdown 远不止这些~~bug？(#･∀･)~~，更多的使用方式请参见 [参考](#参考)

### config

一般来说 Hexo 一共有两个 _config.yml 文件，一个是站点配置文件，一个是主题配置文件，使用时请注意区分，直接进去修改就OK。需要注意的是每一个`:`（冒号）后面一定要有一个空格，使用过程中看到不会的句子时，请善用翻译。以下为此次接触时站点配置文件需要更改的部分。

> 
> | 参数 | 描述 |
> | ---  | :--- |
> | title | 网站标题 |
> | subtitle | 网站副标题 |
> | description | 网站描述 |
> | author | 您的名字 |
> | language | 网站使用的语言 |
> | timezone | 网站时区。Hexo 默认使用您设备的时区。比如说：America/New_York, Japan, 和 UTC 。 |
> | theme | 当前主题名称。值为false时禁用主题 |
> | deploy | 部署部分的设置 |

### 网站压缩

提高网站的加载速度，优化使用体验，使用 neat 进行静态文件压缩。在站点根目录运行：

```
npm install hexo-neat --save
#安装 neat 插件
```

在站点配置文件最后添加

```
# hexo-neat

neat_enable: true

neat_html:
  enable: true
  exclude:
  
neat_css:
  enable: true
  exclude:
    - '*.min.css'

neat_js:
  enable: true
  mangle: true
  output:
  compress:
  exclude:
    - '*.min.js'
```

### PWA

>  PWA(Progressive Web Apps) 是 Google 提出的用前沿的 Web 技术为网页提供 App 般使用体验的一系列方案。
>
>  PWA 本质上是 Web App ，借助一些新技术也具备了 Native App 的一些特性，兼具 Web App 和 Native App 的优点。
>
>  PWA 的主要特点包括下面三点：
>  - 可靠 - 即使在不稳定的网络环境下，也能瞬间加载并展现
>  - 体验 - 快速响应，并且有平滑的动画响应用户的操作
>  - 粘性 - 像设备上的原生应用，具有沉浸式的用户体验，用户可以添加到桌面

简单来说，PWA能够提高你的网站第二次响应的速度，还能让你的网站离线使用。

首先你的网站需要全站 https 访问，然后在站点根目录运行：

```
npm i hexo-offline --save
#安装offline插件
```

在站点配置文件中添加：

```
# offline config passed to sw-precache.
service_worker:
  maximumFileSizeToCacheInBytes: 5242880
  staticFileGlobs:
  - public/**/*.{js,html,css,png,jpg,gif,svg,eot,ttf,woff,woff2}
  stripPrefix: public
  verbose: true
```

然后

```
cd source
#进入source文件夹

vim manifest.json
#新建manifest.json文件并编辑
```

把下面的字符修改后粘贴进去，注意图标放在站点目录的 `source/imsge/` 目录里，或者你也可以使用图床。

还可以选择[App Manifest Generator](https://app-manifest.firebaseapp.com/)，把下载好的文件复制到相应位置即可。

```
{
  "name": "Ākura的笔记本",
  "short_name": "Ākura的笔记本",
  "description": "私のweb",
  "icons": [{
      "src": "https://404gle.cn/images/avatar.gif",
      "sizes": "606x606",
      "type": "image/png"
    }],
  "start_url": "/",
  "scope": "/",
  "display": "fullscreen",
  "orientation": "portrait",
  "background_color": "#f3f3f3",
  "theme_color": "#f3f3f3",
  "related_applications": [],
  "prefer_related_applications": false
}
```

最后需要引入 manifest.json ，因为我使用的是 Next 主题，所以把下面的字符复制进 Next主题 的 head文件 （`站点根目录/themes/next/layout/_custom/header.swig`）中：

```
<link rel="manifest" href="/manifest.json">
```

## 参考

[Daring Fireball: Markdown](https://daringfireball.net/projects/markdown/)

[Termux-ohmyzsh](https://github.com/Cabbagec/termux-ohmyzsh)

[文档 | Hexo](https://hexo.io/zh-cn/docs/) 强烈建议把`Hexo`的文档全部读一遍。