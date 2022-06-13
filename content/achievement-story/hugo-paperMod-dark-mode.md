---
title: Hugo PaperMod 初探，深色模式
date: 2021-07-04T18:00:00+08:00
updated: 2021-07-04T18:00:00+08:00
images: ["images/og/achievement-story/hugo-papermod-dark-mode.png"]
---

深色模式、夜间模式，不管它们叫什么，通常是降低明度、换用深色的主题色以实现人眼在环境光较暗时更好的友好性，19 年 5 月发布的 Android Q Beta 3 正式支持了深色模式[^1]，苹果也在同年的 iOS 13 Beta 2 推出了深色模式[^2]，Windows 上的深色模式则可以追溯到 16 年[^3]。作为现代生成器与主题之一的 Hugo 和 PaperMod 自然也支持这一特性。<!--more-->

W3C 尝试让网页避免 `dark theme`/`dark mode`/`night mode`/`AMOLED mode` 之间的争端，推出了 `prefers-color-scheme` 这一媒体查询规则，但就如在 Android Q 以下装置的 Chrome 会借助省电模式来开启深色模式一样，如何支持更多的设备成了一个问题，如何把新的特性和已有的深色模式结合，又是一个问题。

正如前文[^4]所说的一样，Hugo PaperMod 本质是通过 JavaScript 在 `<body>` 中输出 `.dark` 并根据此切换样式表以切换两种模式。在不支持的浏览器上能够手动切换，在支持 `prefers-color-scheme` 特性的浏览器上也能够手动覆盖显示模式。但当访客在夜间手动切换到了深色模式，第二天白天再次打开网页时依旧会显示深色模式。

解决的方法是把访客手动设定的状态在触发一定条件后清除，最开始想的是与时间相关，但这会需要引出更多的判定，最后发现了苏卡卡的解决方案[^5]：当用户设定的状态和设备状态相同时清除状态。复制主题中的 `header.html` 到博客根目录下，并在第 27 行后新增以下 JavaScript 片段。

```javascript
localStorage.clear(pref-theme);
```

请注意在 27 行后添加换行。

[^1]:https://developer.android.com/about/versions/10/highlights
[^2]:https://www.apple.com/newsroom/2019/06/apple-previews-ios-13/
[^3]:https://blogs.windows.com/windowsexperience/2016/08/08/windows-10-tip-personalize-your-pc-by-enabling-the-dark-theme/
[^4]:https://akuraito.cn/essay/switch-to-hugo/
[^5]:https://blog.skk.moe/post/hello-darkmode-my-old-friend/

