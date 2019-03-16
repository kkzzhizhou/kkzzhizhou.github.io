---
title: RSS订阅和阅读简明教程
date: 2017-7-3
updated: 2018-9-3 18:18:37
tags: [rss,信息聚合，效率生活]
categories: Web技术
---
## 更新日志

- 2018-9-3：
  - 更新图片为国内图床
  - 更新比较完美的微博RSS订阅的方法：方法三
  - 完善微信公众号全文RSS订阅的方法：irreader+feed43
  - 更新Twitter全文RSS订阅的方法：twitrss.me
  - 更新irreader的简述
- 2018-8-27：更新irreader(一款本地播客，RSS阅读工具)
- 2018-8-20：更新制作RSS Feed的方法
- 2018-8-8：更改排版，更新提供全文输出RSS的网站，增加提供RSS生成制作的网站
- 2018-7-7：更新RSSHub中大部分主流网站，重新排版文章，删除过时和错误的方法。
- 2017-7-3：更新全文输出网站freefullrss

## RSS是什么？

![](https://ws1.sinaimg.cn/large/d22ff2eely1fuwihyhsj3j20qo0dcaby.jpg)
> RSS是一种内容信息聚合技术。简单点讲，你可以订阅自己关心的内容，例如博客，视频网站，知乎，简书，微信公众号，播客，门户网站等，当内容更新时自动同步到阅读器中，最终所有信息汇总到一个应用里查看阅读。

## 在线RSS阅读软件：[inoreader](http://www.inoreader.com/) 

推荐指数：⭐️⭐️⭐️⭐️

一款类似Google Reader的RSS阅读器，阅读器支持平台包括Web,Android,iOS。

接近两年的使用inoreader，让人深刻的意识到inoreader在阅读体验上很是糟糕。

## 本地RSS阅读软件：[irreader](http://irreader.netqon.com/)

推荐指数：⭐️⭐️⭐️⭐️

适用于以下的场景：

1. 有些订阅源在inoreader阅读无法全文输出，不方便。比如：http://www.dayanzai.me/feed
2. 有些订阅源虽然是即使全文输出，但图片反盗链。比如：http://www.ixiqi.com/feed
3. 有些想订阅的源却不提供订阅地址，比如：http://www.macbl.com/
4. 使用inoreader免费版用户有广告
5. 使用Inoreader时阅读区域无法调整
6. 使用inoreader没有阅读模式
7. 想要一边看RSS一边收听播客

以上的场景irreader通过以下方式完美的解决：

1. irreader直接模拟浏览器打开链接，全文输出完美，排版优秀，图片正常加载。
2. **irreader支持订阅HTML静态地址。**
3. irreader内置Adblock，自动过滤网页广告和弹窗。
4. 相比inoreader至多一半的屏幕用于阅读文章，irreader阅读区域最多能占到屏幕的4/5
5. irreader内置阅读模式插件
6. irreader内置播客订阅

存在的不足：

1. 缺少同步功能
2. 缺少信息过滤功能

总结：作为inoreader的长期使用者，深知inoreader的种种不足，现在有了irreader，用来弥补inoreader，再合适不过了。

## RSS订阅工具：[RSSHub](https://docs.rsshub.app/)

推荐指数：⭐️⭐️⭐️⭐️⭐️

网站集成了主流网站的订阅方式，很强大。

当然这网站也不是万能的，有特殊需求的需要自己制作RSS Feed。

<!-- more --> 

## 如何订阅RSS?

### 1. 一般方法

#### 1.1  在网站首页中寻找RSS订阅按钮(有时候需要仔细找找)

一般博客网站如CSDN，新浪博客，Wordpress博客等都会有RSS订阅按钮用来获取订阅地址。

![](https://ws1.sinaimg.cn/large/d22ff2eely1fuwiqx2fktj20cn02n74t.jpg)



#### 1.2 在网址后面输入feed，或者atom.xml，或者rss

> 殁漂遥：https://www.laomoit.com/
>
> 订阅地址：https://www.laomoit.com/feed

> HI,DIYGOD：https://diygod.me/
>
> 订阅地址：https://diygod.me/atom.xml

> 网易博客：http://xiangkg.blog.163.com/
>
> 订阅地址：http://xiangkg.blog.163.com/rss

### 2. 特殊方式订阅主流信息源

#### 微信公众号

##### 方式一：https://rsshub.app/jike/topic/{uid}

参数:

- id, 参考 [即刻-主题-精选](https://docs.rsshub.app/#%E4%B8%BB%E9%A2%98-%E7%B2%BE%E9%80%89)

推荐指数：⭐️⭐️⭐️⭐️

##### 改进方法：feed43+irreader全文阅读

原本的订阅地址中，标题并不是微信原文链接，可以通过feed43进行标题地址改造。以丁香园为例，方法如下图：

![](https://ws1.sinaimg.cn/large/d22ff2eely1fuwi7o7l6jj20j627madd.jpg)

##### 方法二：https://rsshub.app/wechat/wasi/{uid}

参数:

- id, 瓦斯公众号 id, 可在[瓦斯](https://w.qnmlgb.tech/wx)搜索公众号, 打开公众号页, 在 URL 中找到 id

推荐指数：⭐️⭐️⭐️⭐️

方法二标题就是原文链接，无须像方法一通过Feed43改造。但目前支持的公众号比较少。

#### 微博

##### 方法一：https://rsshub.app/weibo/user/{uid}

推荐指数：⭐️⭐️⭐️

##### 方法二：https://rsshub.app/weibo/user2/{uid}

方法一获取 V+ 付费博主会有数据缺失, 所以这里提供另外一种方式, 这种方式的缺点是描述不如上面的完善, 建议优先选择第一种方案

推荐指数：⭐️⭐️⭐️

##### 方法三：https://api.izgq.net/weibo/rss/{uid}

方法一和方法二中微博订阅不能显示全文，并且更新不及时。

推荐指数：⭐️⭐️⭐️⭐️⭐️

- uid, 用户 id, 博主主页打开控制台执行 `/uid=(\d+)/. exec(document.querySelector('.opt_box .btn_bed').getAttribute('action-data'))[1]` 获取

#### 知乎

> 服务地址：https://rss.lilydjwg.me/
>
> 服务地址2:https://docs.rsshub.app/#%E7%9F%A5%E4%B9%8E

#### 百度贴吧

> 服务地址：https://docs.rsshub.app/#%E8%B4%B4%E5%90%A7

#### 简书

> 服务地址：http://jianshu.milkythinking.com/
>
> 服务地址2：https://docs.rsshub.app/#%E7%AE%80%E4%B9%A6

#### Twitter

##### 方法一：https://rsshub.app/twitter/user/{uid}

参数:

- id, 用户 id，比如https://rsshub.app/twitter/user/ruanyf

推荐星数：⭐️⭐️⭐️⭐️

##### 方法二：https://twitrss.me/twitter_user_to_rss/?user={uid}

参数:

- id, 用户 id，比如https://twitrss.me/twitter_user_to_rss/?user=ruanyf

推荐星数：⭐️⭐️⭐️⭐️

#### Facebook

> 服务地址：https://fbfeed.github.io/

#### 即刻

> 服务地址：https://docs.rsshub.app/#%E5%8D%B3%E5%88%BB

#### 掘金

> 服务地址：https://docs.rsshub.app/#%E6%8E%98%E9%87%91

#### 豆瓣

> 服务地址：https://docs.rsshub.app/#%E8%B1%86%E7%93%A3

#### 今日头条

> 服务地址：https://docs.rsshub.app/#%E4%BB%8A%E6%97%A5%E5%A4%B4%E6%9D%A1

#### Instagram

> 服务地址：https://docs.rsshub.app/#instagram

#### V2EX

> 服务地址：https://docs.rsshub.app/#v2ex

#### Telegram

> 服务地址：https://docs.rsshub.app/#telegram

#### Github

> 服务地址：https://docs.rsshub.app/#github

#### 什么值得买

> 服务地址：https://docs.rsshub.app/#%E4%BB%80%E4%B9%88%E5%80%BC%E5%BE%97%E4%B9%B0

#### 灵梦御所

> 服务地址：https://docs.rsshub.app/#%E7%81%B5%E6%A2%A6%E5%BE%A1%E6%89%80

#### 草榴社区

> 服务地址：https://docs.rsshub.app/#%E8%8D%89%E6%A6%B4%E7%A4%BE%E5%8C%BA

### 3. 订阅视频（追番，追剧，追综艺）

#### 优酷

1.  进入用户首页，查看源代码，搜索关键字“user_id”，如“UNDQ3MTU0MDI4”，去掉第一个字母U，得到用户代码如“NDQ3MTU0MDI4”。     
2.  将用户代码进行BASE64解密，得到用户识别码，网址：http://tool.chinaz.com/Tools/Base64.aspx 如“NDQ3MTU0MDI4”解密为447154028。将用户识别除以4，得到用户真实ID，如447154028/4=111788507。 
3.  用于订阅的RSS地址为 http://www.youku.com/user/rss/id/{用户真实ID}, 如 http://www.youku.com/user/rss/id/111788507
现在可以在源代码中搜索“ownerId”，直接获得用户真实ID
#### Youtube

> 方式：将视频主首页地址粘贴到inoreader中，就能成功订阅了。
>
> 服务地址：https://docs.rsshub.app/#youtube
>
> 举例：https://www.youtube.com/channel/UCvAFi3Brfyci4XH7V3pGcpA

#### 爱奇艺

> 服务地址：https://docs.rsshub.app/#%E7%88%B1%E5%A5%87%E8%89%BA

#### blibili

> 订阅up主：https://api.prprpr.me/bilibili2rss/user/{user_ID}
>
> 订阅番剧：https://api.prprpr.me/bilibili2rss/bangumi/{bangumi_ID}
>
> 订阅分区：https://api.prprpr.me/bilibili2rss/partion/{partion_ID}
>
> 服务地址2：https://docs.rsshub.app/#bilibili

### 4. 订阅播客
#### 订阅喜马拉雅
> 服务地址：https://docs.rsshub.app/#%E5%96%9C%E9%A9%AC%E6%8B%89%E9%9B%85
#### 订阅网易云音乐

> 服务地址：https://docs.rsshub.app/#%E7%BD%91%E6%98%93%E4%BA%91%E9%9F%B3%E4%B9%90



## 制作RSS Feed

### 方法一：Feed43（免费）

官网：http://feed43.com/   

推荐指数：⭐️⭐️⭐️

教程：[FEED43新手教程：为任意网页定制RSS格式订阅源](https://post.smzdm.com/p/553684/)

### 方法二：Fivefilters Feed Creator（免费）

官网：http://createfeed.fivefilters.org/index.php

推荐指数：⭐️⭐️⭐️⭐️⭐️

1. “Enter web page URL”就是输入网页网址，例如https://www.ipcfun.com/

2. “Look for links inside HTML elements whose id or class attribute contains” 根据ID或Class筛选元素，例如entry-title

3. “Only keep links if link URL contains”URL过滤，仅保留包含指定字符串的链接，例如html

   ![Fivefilters Feed Creator](https://lh3.googleusercontent.com/-a7lS-uENCys/W3o__82ASOI/AAAAAAAAee8/Hbs8R92korgd-2OiVCSxCGXRp37AznXnQCHMYCw/s0/chrome_2018-08-20_12-13-49.jpg)

### 方法三：Fetchrss(免费限制数量5个)

官网：http://fetchrss.com/ 

推荐指数：⭐️⭐️⭐️⭐️

GUI界面操作，非常简单易懂。

New item：选择一篇文章区域

Headline：选择文章的标题

Summary：选择文章的概述

Illustration：选择文章的插画（可选项）

Date：选择文章的日期（可选项）

Author：选择文章的作者（可选项）

Link：选择文章的链接（可选项）

## 特例

1. http://www.vxia.net/rss.php无法订阅

这种rss.php结尾的feed地址，Inoreader无法正常订阅，但Feedly可以正常订阅。

2. http://www.dayanzai.me/feed无法全文输出

这种博客网站很特别,需要使用Feed43对其Feed地址重新输出成xml订阅地址后就可以正常全文输出了



## RSS阅读体验

### 全文输出

提供转换为全文输出的网站

1.  [fullcontentrss](http://fullcontentrss.com/)  推荐指数：⭐️⭐️⭐️⭐️⭐️
2.  [FeedEx.net](https://feedex.net/)       推荐指数：⭐️⭐️⭐️⭐️
3.  [Full-Text RSS](http://ftr.fivefilters.org/)    推荐指数：⭐️⭐️⭐️
4.  [freefullrss](https://www.freefullrss.com/)        推荐指数：⭐️⭐️⭐️

### 信息过滤

当RSS内容既包含你想要的内容，也有一些不想看到的内容，需要使用关键字过滤。

1. inoreader非付费用户只能过滤一个订阅源。
2. 如果需要大量过滤，可以尝试搭建**Tiny Tiny RSS**。

## RSS原理延伸

### 1. 场景一

在某个卖二手论坛里经常出现性价比很高的二手货，正好你最近有想买的IPad 2，你想有一个工具，当论坛里出现有想要的IPad 2的时候自动提醒你，让你能够以最快的速度入手。

解决方法：[网页更新提醒工具](https://play.google.com/store/apps/details?id=me.webalert&hl=zh-CN)

使用方法：软件记录的网页操作，并到你的选定的网址中监测某些网页元素的变动，一有变动，就可以提醒。

#### 2. 场景二

在淘宝，天猫，京东等一些购物网站一些物品价格经常价格变动，我们想以比较低的价格入手，便需要了解价格的实时变动信息，并在价格低于自己预期的时候购买。

解决方法：惠惠购物助手

使用方法：在手机端和浏览器端安装惠惠购物助手。将自己关心的商品放入惠惠助手的购物车中，在软件中可设置价格。当价格低于某一数值时，手机端发出提醒。

#### 3. 场景三

“如果天气晴朗，提醒我晒被子。”用英语将句式提取出来就是If this then that.生活中很多这种判断，如果这种判断能用软件实现那该多好。

解决方法：IFTTT(安卓，Web)

使用方法：在软件添加各种条件和结果，满足条件时自动执行。

#### 4. 场景四

逢年过节，总是要抢车票。到了回家前几天，票总是被一扫而空。但心想也许会有人退票，那你可能需要一款软件能够实时检测余票，并提醒你。

解决方法：智行

使用方法：本地云监控，发现有余票即时提醒。