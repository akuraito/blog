---
title: 我与我的设备-Motorola Edge S Pro
date: 2022-01-18 21:54:00
updated: 2022-01-18 21:54:00
categories: ["toss"]
---

21 年的手机市场此起彼伏，国行 Nokia 摆烂不断，8.3 5G 或成为廉价版 Pixel 5，没想到继承遗志的重任兜兜转转交到了 Motorola Lenovo 手中。<!--more-->

## 缘起

上次写手机设备还是19 年的 [Nokia 7](../with-my-nokia-7/)，羸弱的 635 在 QQ 还没硬塞 UE 的时候就显得力不从心，只好光速回退 Play 版。同样是 19 年进行了最后一次更新，不得不说，很配。没搞到星星星的防爆盾，也没收到 N9 的消息，唯一让人眼前一亮的作品竟然是 2720 Flip[^1]。全球手机市场同样多灾多难，打孔、药丸、刘海轮番上阵，屏下摄像头缺点仍旧明显，但也比这些好了不少，折叠屏方面的最爱是星星星的 Galaxy Z Flip，但始终没有一台真正想要的新机，不得不说是一种悲哀。

旧手机命数已到，总得找找有没有能凑合的吧，恰逢超高性价比的 moto edge x 30 和 s 30 发布会，一台是 8 Gen 1，一台是 888Plus，现在看来幸好没有购入。至于 Motorola 在 21 年最早进入视线的则是年初的 edge s，同样是超高性价比的 870 似乎可以和红米打一架。我对手机的要求也从年初不断下降到 2000 CNY、170g 的 7 系，成为了妥协的最低标准。edge s 也因为 Motorola Edge s Pro 和轻奢版的发布而开启了直降500元的活动，可惜当我想要动手的时候已经基本卖完，这就是当时 2000 元市场的唯一选择。而 edge s pro 也成功在 x 30 和 s 30 发售之后再次降价，充分印证了那句老话：早买早享受，晚买享折扣。

但不要忘了最重要的一点，类原生与魔改。一加在脱离了大氢之后，彻底被排除在备选项之外，这是 Moto 和 Nokia 的悲哀，市场空位的负反馈造成了研发人员的缺失，同时也迫使他们只能完成最基础的工作，而这恰恰是我所喜欢的特点，辛辣又讽刺。当然联想还是有着一些 Z UI 的底子在，比起当初的 Nokia 好了不少，只是这种积累，是好是坏？

## 外观

作为主打性价比的机型，edge s pro 的全身都透露着这么一个词：不讲究。这是近年手机的通病，首先来讲讲宣传图上能够一眼看出来的东西：顶部居中的打孔、三面等边框、还有一方二圆的镜头模组。这些都可以用爱去包容，但不讲究可不会跟你说这么多，凑合凑合得了。

拿到手机开机第一眼看见的肯定是屏幕，和他四边的圆角。很难想象 Google 直到 Android 12(API 31) 才推出了 getRoundedCorner[^2] 参数，这意味着手机里的软件直到今天也不知道手机到底是长啥样的，只能查询数据库或尝试兼容性写法。圆角的出现是全面屏的必然，不管是为了刚性、手感或是潮流，没有谁想做圆滑当道时代的尖锐异类。打孔的表现更是灾难，竖屏时还好，一旦切换到横屏就开始百花齐放，`LAYOUT_IN_DISPLAY_CUTOUT_MODE` 也会带来各种问题，尽管对界面元素的遮挡范围不大，但只要遮住一个就很糟心，横屏下显示三页图块（Tile）时居然会被吃掉代表第三页的圆点。

看完了屏幕，来看看中框上不在一条线上的开孔，尤其是电源孔位，偏的离谱。最后要隆重介绍的则是不讲究到极点的镜头模组，一共居然分了四层！最外是一层金属边框，其中包裹着分为两层的镜头矩阵，较矮的一层安装了同色的暖光灯双闪与麦克风，至于镜头本身则又升高了一层。主摄和微距都不在正中，长焦居然还有一条缝！

而这台手机在外观上为数不多的优点竟然是直屏和玻璃夹金属的三明治结构，很难相信这些本该做好的事会如此难寻。

![比屏幕稍窄的界面、微博极速版横屏播放视频、开孔不在一条线上的底部中框](/images/with-my-motorola-edge-s-pro/slim-content-video-play-bottom.webp)

## 系统

脱离了 Android 9，加入 Android 11。最大的变化自然是 API 30，文件目录干净了好多，自带桌面能满足基本需求，但图标包和字体需要使用联想乐商店才能下载使用，其他都是一股原生味。系统自带 Play 服务开关，但基于国行的特殊性，Play 商店无法更新自己，这点请务必注意。Android 11 的猫猫也很好玩！

显示刷新率有 60 Hz、144 Hz 和自动可选，虽然自动刷新率的描述是使用 AI 以始终保持理想的刷新率，但是他只会锁在120 帧，可能只有少数几个\*\*\*的软件与游戏才能调用 AI 吧。

另外 Motorola 的博客[^3]显示 edge 20 pro（edge s pro 的海外版）会有 Android 12 更新，所以一起期待一下。

![Target API](/images/with-my-motorola-edge-s-pro/target-api.webp)

## 性能

19年还说过音游人不需要高性能，结果雷亚就给我当头一棒，这下我换了 870 总不会再卡了吧？事实证明雷亚之下，众生平等，打开花语旋律的时间最少也得半分钟。至于 RAM 为 8 G 加上模拟的 3 G，就算把这 3 G 全都分给塞了 UE 的 QQ 也绰绰有余，还能体验一下微信秒开的感觉。

## 本地化

联想的本地化再次立大功，基础的应用都达到了能用的水平（Z UI 遗产）除了计算器的交互不太喜欢之外，与我的使用习惯没有大的差别。

### 短信

区别最大的自然是短信，没有加上一堆广告，能识别中文验证码，短信归类，无疑是市场上的一股清流。终于可以抛弃在国内半残的 Google messager 了。另外把聚合通信（Rich Communication Services）翻译成 5G消息 的是哪个人才？

### 负一屏

负一屏的表现和 Nokia HMD 大差不差，都属于食之无用，弃之可惜，所以直接关闭。

### 游戏模式

在游戏模式下可以打开 QQ 与微信的小窗，在开发者选项中其实可以打开相关设置使得所有应用都能以小窗显示，但只能用于桌面。最有用的是关闭通知，但勿扰模式好像更有用一点，所以果不其然，这个功能也被封存。

### 后台策略

划卡即停，默认允许 QQ 和微信后台运行，啊，熟悉的感觉，需要在手机管家（`com.motorola.deviceguard`）的后台运行和应用自启中管理，我选择了打开 Microsoft To Do 和 Microsoft Authenticator，前者用来使桌面小部件保活，后者则是为了管理密码。

### 权限管理

权限管理大概是最讨厌的一项本地化改动，所有的直接点击都会被重定向到手机管家的页面进行管理，看起来是件好事，但一旦想管理`文件与媒体`权限，就会发现他只有 3 个选项：开启、关闭和询问，`仅允许访问媒体文件`权限则需要在设置应用中手动搜索`文件与媒体`才能打开相关界面。强烈推荐使用带有 AppOps 功能的软件来管理权限。

## 杂项

定位使用了百度的服务

没事不要手贱用 Play 商店 升级系统应用

[^1]: https://www.nokia.com/phones/zh_int/nokia-2720
[^2]:https://developer.android.com/reference/android/view/WindowInsets?hl=zh-cn#getRoundedCorner(int)
[^3]:https://www.motorola.com/blog/post?id=387