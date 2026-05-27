---
title: 我与我的设备-破烂服务器
date: 2026-04-26T23:00:00+08:00
updated: 2026-04-26T23:00:00+08:00
categories: ["toss"]
tags: ["Server","Cloudflare","1Panel"]
images: ["images/og/with-my-saba-nanba-zerozeroichi.jpg"]
---

上次对服务器心动还是马斯克收购推特，时间线上不少人转去了 [Misskey](https://misskey-hub.net/cn/)、[Mastodon](https://joinmastodon.org/)，当时去看了看 Mastodon 的文档，只是觉得服务器安全刻不容缓就放下了。直到 25 年黑五刷到十刀一年，2C 1G 20G 的 [CloudCone](https://cloudcone.com/) 灵车，正好碰上几个月前微软为了推 Edge 而[停止了 Authenticator 对自动填充的支持](https://support.microsoft.com/zh-CN/authenticator/changes-to-microsoft-authenticator-autofill)，不如自己搭个 [Bitwarden](https://bitwarden.com/)。<!--more-->

写到一半发现又写成了 Step by step guide，最后还是删删改改，不要这么复杂。


## 服务器选购

第一台服务器关注下服务器在不在国内和付款方式就行，国内服务器绑定域名需要备案。当然其他还有线路啊工单支持啊服务器质量啊等等等等，可以去几个知名服务器论坛逛逛。

虽然不能这么算，但灵车被叫做灵车是有原因的：[Major incident: Hypervisor Outage | Status Page](https://status.cloudcone.com/incidents/346624)。26 年一月下旬，CloudCone 位于洛杉矶的机房发生了 Hypervisor Outage 事故，**所有文件无法恢复**，洛杉矶服务器的优点是国内访问速度会快不少，用的人据说还挺多的，结果这次炸没了。我的服务器在圣路易斯倒是未受到影响。而我选择圣路易斯则是因为本就准备把所有服务放在 Cloudflare CDN 上，避开热门大区也有助于降低遇见超售的概率。

情况就是这么个情况，灵车也不是一定会炸，只是这次炸了个大的。互联网炸是常态，就连 Cloudflare 炸的次数也不少，遇到了就是遇到了，没办法就是没办法，最后还得靠厂商的赔偿说话。灵车的赔偿本就一般，更别说文件全丢，自己能做的也就只有谨记 321 多搞点备份。

虽然已经对现在这个小服务器感到嫌弃了，但毕竟还是刚开箱没几个月，等下次黑五再换。如果你恰巧想买个服务器，这里列几个大厂~~和灵车~~，除此之外还有许多大厂小厂，挑个喜欢的就行。

- 国内大厂
    - [阿里云](https://www.aliyun.com/)、[aff（仅新用户可用）](https://www.aliyun.com/minisite/goods?userCode=voyp9fs0)
    - [腾讯云](https://cloud.tencent.com/)、[aff](https://curl.qcloud.com/SeUk8TyP)
- 国外大厂
    - [AWS](https://aws.amazon.com/cn/)
    - [Azure](https://azure.microsoft.com/zh-cn/)

## SSH

购买服务器之后第一件事自然就是：改 SSH 端口号&关闭密码登录（也可以等 1Panel 安装好之后直接在面板里改）

IPv4 地址每天都在被脚本小子暴力扫描，只要还开着22端口，就会看见一堆 IP 先用密码试一下 root，再用密钥试一下 user，然后就开始慢慢试密码，深刻怀疑脚本小子用的都是同一份脚本。

## 1Panel

作为半吊子开源灵车爱好者，我对 SSH 终端的需求就是不知道自己有什么需求，对服务器管理自然也是找个面板完事。顺手摸出来一个终端，自己常用的是 [Termux](../code-server-on-termux/) 和 WSL。如果摸不出来，可以试试 [Tabby](https://tabby.sh/)。登录后执行此命令以安装 1Panel，一路回车后使用终端输出的登录地址、账号密码即可登录面板。[1Panel 官网](https://1panel.cn/)亦有视频教程。

```
bash -c "$(curl -sSL https://resource.fit2cloud.com/1panel/package/v2/quick_start.sh)"
```

进面板之后点击`系统`-`SSH 管理`即可找到改 SSH 端口号&关闭密码登录的选项了，改完之后还得在`系统`-`防火墙`把 SSH 的端口打开，改完端口之后是一个脚本小子也没遇到，世界瞬间清净许多。如果觉得还不放心的话，点击`工具箱`-`Fail2ban`，自行按提示安装。

同时为了防止包括但不限于自己玩炸了，AI 玩炸了，机房被热武器攻击等情况，勤于备份是个好习惯。先去`面板设置`-`备份账号`添加账号，再去`计划任务`创建`系统快照`任务，若有需要，之后的`应用备份`和`同步 WAF IP 组任务`也在此处设置。最开始用的是坚果云，结果后来快照体积越来越大，超过了单个文件的上传大小，于是换成了 OneDrive。

1Panel 有一套自动申请证书的机制，但为了保护服务器 IP 加上 Cloudflare 重度依赖，选择了 Cloudflare 的源服务器证书，登录 Cloudflare 后点击已有的域名，再点击 `SSL /TLS`-`Origin Server`-`Create Certificate`，按照说明填完即可，至于时间则直接选择15年。完成后把私钥和证书复制到面板的`网站`-`证书`-`上传证书`处，后续创建网站时选用即可。

既然已经用了 Cloudflare 源服务器证书，那自然要顺手把其他来源的访问全关掉。1Panel 免费版的 WAF 提供了部分功能，点击`WAF`-`黑白名单`-`IP 组`-`创建`，把 Cloudflare [IP Ranges](https://www.cloudflare.com/ips/) 列出的 [IPv4 text list](https://www.cloudflare.com/ips-v4/#) 和 [IPv6 text list](https://www.cloudflare.com/ips-v6/#) 填入即可，导入方式选择远程下载。在`WAF`-`黑白名单`-`IP`-`白名单`中添加此 IP 组，黑名单中添加 IPV4 范围 `0.0.0.0-255.255.255.255`。为了防止 Cloudflare 更新 IP 范围，还需要在计划任务添加`同步 WAF IP 组`任务。

当然这也不是没有缺点的：

> [请注意 这个配置无法与 WAF CDN 设置一起用 需要关闭 CDN 的开关](https://bbs.fit2cloud.com/t/topic/7131#:~:text=%E8%AF%B7%E6%B3%A8%E6%84%8F%20%E8%BF%99%E4%B8%AA%E9%85%8D%E7%BD%AE%E6%97%A0%E6%B3%95%E4%B8%8E%20WAF%20CDN%20%E8%AE%BE%E7%BD%AE%E4%B8%80%E8%B5%B7%E7%94%A8%20%E9%9C%80%E8%A6%81%E5%85%B3%E9%97%AD%20CDN%20%E7%9A%84%E5%BC%80%E5%85%B3)

而且显然不符合 WAF 的哲学：

> [WAF 不应该去处理 CDN IP ，应该是获取用户的真实访问 IP](https://bbs.fit2cloud.com/t/topic/5310#:~:text=WAF%20%E4%B8%8D%E5%BA%94%E8%AF%A5%E5%8E%BB%E5%A4%84%E7%90%86%20CDN%20IP%20%EF%BC%8C%E5%BA%94%E8%AF%A5%E6%98%AF%E8%8E%B7%E5%8F%96%E7%94%A8%E6%88%B7%E7%9A%84%E7%9C%9F%E5%AE%9E%E8%AE%BF%E9%97%AE%20IP)

为了保护 IP 可谓是绞尽脑汁，如果以上还不够？[我还找到更多](https://www.typemylife.com/1panel-cloudflare-wordpress-origin-server-ip-protection/)。

### 网站

万事俱备，那自然要先顺手……把面板绑域名上。先在 Cloudflare `域名`-`DNS`-`Records` 添加一个新的 `A`/`AAAA` 记录指向服务器的 IP 地址并勾选`Proxy`，在面板`网站`-`网站`-`创建`中创建反向代理，域名填刚刚新建的域名，代理地址填 127.0.0.1:<1panel的端口>。做完这些之后还可以在`面板设置`-`安全`-`域名绑定`中填写相应域名。

### Bitwarden

真是绕了好大一圈，是时候安装 Bitwarden 了，`应用商店`-`全部`搜索 Bitwarden 即可安装，取消勾选`端口外部访问`使其仅能通过域名访问，仿照前文给 Bitwarden 也绑个域名，创建时选择一键部署。

装好之后打开一看，你怎么叫做 [Vaultwarden](https://github.com/dani-garcia/vaultwarden) 啊？Vaultwarden 是 Bitwarden 服务器端的第三方实现，适配大部分功能，最大的区别是资源占用会小许多，也是大部分人安装 Bitwarden 的首选，但在应用商店直接叫做 Bitwarden 还是太离谱了。管理界面默认是没有开的，参考 [Enabling admin page](https://github.com/dani-garcia/vaultwarden/wiki/Enabling-admin-page)，然后在`容器`-`容器`-`更多`-`编辑`-`标签 & 环境变量`处添加以下环境变量：

```
Vaultwarden_ADMIN_TOKEN='$argon2id$v=19$m=65540,t=3,p=4$MmeK.....'
```

写本文的时候再去看了看，结果环境变量里已经消失了，倒是还能打开，也能在管理页面更改管理密码，应该是更新的时候被 1Panel 初始化了，还好 Vaultwarden 会自己保存。

### Miniflux

Vaultwarden 装好之后，看着空空的服务器总不是滋味，有什么软件日常用得上又需要一直在线呢？思来想去总算找到，就是你了，[Miniflux](https://miniflux.app/)！在应用商店先安装 postgresql，再安装 Miniflux 即可。

之前是直接用了 Miniflux 官网上的 Compose 文件，结果在安装应用商店版后直接把`容器`-`编排`页面的旧 Miniflux 覆盖了，好在卸载商店版后能恢复。使用商店版的同时我还改了一些设置：[Configuration Parameters](https://miniflux.app/docs/configuration.html)，因此在更新时需要手动更改 Compose 文件，还挺麻烦。

```diff
services:
    miniflux:
        environment:
+++         # 设置 Miniflux 的域名
+++         - BASE_URL=https://miniflux.example.com/
+++         # 清理旧条目的时间
+++         - CLEANUP_FREQUENCY_HOURS=9600
+++         - CLEANUP_ARCHIVE_READ_DAYS=400
+++         - CLEANUP_ARCHIVE_UNREAD_DAYS=400
+++         # 代理条目中的图片
+++         - MEDIA_PROXY_MODE=all
+++         - MEDIA_PROXY_PRIVATE_KEY=example
```

Miniflux 的获取全文功能有时会把广告内容一起存下来，这时就要用到 [Content Rewrite Rules](https://miniflux.app/docs/rules.html#rewrite-rules)，当然以我贫瘠的 web 水平，还是选择打开 uBlock Origin 记录器，复制对应的元素过滤规则。

### RactFlux

手机上常备的 RSS 阅读器是 [Read You](https://github.com/ReadYouApp/ReadYou)，既然有了 Miniflux，刚好开启`设置`-`集成`-`Google Reader`功能，可惜有条目乱窜的 BUG :point_down:

![条目串门](/images/with-my-saba-nanba-zerozeroichi/read-you-with-miniflux.webp)

找来找去，找到了 [RactFlux](https://github.com/electh/ReactFlux)。在 1Panel `容器`-`编排`-`创建`粘贴以下内容：

```
services:
    reactflux:
        image: electh/reactflux
        container_name: reactflux
        restart: always
        ports:
            # 设置为 127.0.0.1 阻止通过 IP 访问
            - 127.0.0.1:2000:2000
```

### 其他

我一直用 [Heimdallr](https://github.com/LeslieLeung/heimdallr) 来转发各种通知，但在 [Vercel](https://vercel.com/) 网页上改环境变量还是太痛苦了，顺便也迁移到服务器上来。

搭配使用的还有 [TediCross](https://github.com/TediCross/TediCross) 用于同步消息，[Gotify](https://gotify.net/) 配合 [gotify-webhook](https://github.com/wuxs/gotify-webhook) 将只支持 Gotify 的通知转发到 Heimdallr。

## 最后

下次黑五换个能运行 Mastodon 的服务器。