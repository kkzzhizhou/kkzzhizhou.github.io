---
title: RSS订阅和阅读简明教程
tags:
  - 效率生活
categories: 
- [技术]
toc: false
abbrlink: rss-tutorial
date: 2017-07-03 00:00:00
updated: 2020-3-17 11:49:49
---

## RSS是什么？

![](/pic/rss-tutorial-1.jpg)
> RSS是一种内容信息聚合技术。简单点讲，你可以订阅自己关心的内容，例如博客，视频网站，知乎，简书，微信公众号，播客，门户网站等，当内容更新时自动同步到阅读器中，最终所有信息汇总到一个应用里查看阅读。

<!-- more --> 

## 开始使用RSS

1. 使用电脑端Chrome打开[inoreader](http://www.inoreader.com/),注册一个账号
2. 注册成功且登录之后，点击搜索按钮，输出本博客的订阅地址：https://blog.ziiyc.com/atom.xml, 如下图所示,选中之后点击右上角的订阅即可

![](/pic/rss-tutorial-4.jpg)

## 在线RSS阅读软件：[inoreader](http://www.inoreader.com/) 

一款类似Google Reader的RSS阅读器，阅读器支持平台包括Web,Android,iOS。

~~接近两年的使用inoreader，让人深刻的意识到inoreader在阅读体验上很是糟糕。~~

使用inoreader接近四年，阅读体验近期有了一些改观，虽谈不上舒适，但也是可以比较正常使用了，比如添加了阅读区域手动调整功能。

## 谈谈其他RSS阅读软件使用体验

- [irreader](http://irreader.netqon.com/)
这个阅读工具近期不怎么更新了，从阅读体验上看是很不错的，但没有同步，没有手机端, 缺少信息过滤功能

- [feedly](https://feedly.com/)
使用过一段时间，功能够用，界面美观，需要科学上网，缺点是收费贵。

- [Tiny Tiny RSS](https://tt-rss.org/)
自建rss阅读服务器方案，从全文阅读，繁体转简体，文章过滤等功能脚本看，应有尽有，但实际阅读体验不佳，手机端可用软件匮乏，且质量不怎么样。网页端阅读使用Google Reader主题算是美观。

- [feedbro](https://nodetics.com/feedbro/)
浏览器rss阅读方案，支持Chrome，Firefox主流浏览器，在阅读体验是可以说是最优秀的，因为运行环境是浏览器，所以不会出现订阅源常见的没有全文，图片显示不全的问题。遗憾的有两点，一是不支持任意形式同步，二是不支持其他终端，比如Web端、手机端。

## 如何订阅RSS?

### 1. Tampermonkey + RSS+

[Tampermonkey](https://chrome.google.com/webstore/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo?hl=zh-CN)

[RSS+](https://greasyfork.org/zh-CN/scripts/373252-rss-show-site-all-rss)

![rss+](/pic/rss-tutorial-2.jpg)

### 2. 浏览器插件：RSSHub

支持显示RSSHub网站支持的订阅地址直接显示

### 3. 第三方订阅服务

- [rsshub](https://docs.rsshub.app/): 网站集成了主流网站的订阅方式，很强大，不断更新 推荐指数：⭐️⭐️⭐️⭐️⭐️
- 微博: https://api.izgq.net/weibo/rss/{uid} 推荐指数：⭐️⭐️⭐️⭐️⭐️
PS: uid, 用户 id, 博主主页打开控制台执行 `/uid=(\d+)/. exec(document.querySelector('.opt_box .btn_bed').getAttribute('action-data'))[1]` 获取
- 知乎: https://rss.lilydjwg.me/ 推荐指数：⭐️⭐️⭐️⭐️
- 简书: http://jianshu.milkythinking.com/ 推荐指数：⭐️⭐️⭐️⭐️
- Twitter: https://twitrss.me/twitter_user_to_rss/?user={uid} 推荐指数：⭐️⭐️⭐️⭐️
- Facebook: https://fbfeed.github.io/ 推荐指数：⭐️⭐️⭐️⭐️

## RSS进阶

### RSS全文输出

#### 自建服务器方案

- [rss2full](https://github.com/feedocean/rss2full) 推荐指数：⭐️⭐️⭐️⭐️
大部分情况可以得到一个不错的全文输出效果,举例：http://www.xingkbjm.com/feed

- [tiny tiny rss + mercury](https://tt-rss.org/) 推荐指数：⭐️⭐️
这种方式是通过调用mercury生成全文方式，需要搭建mercury服务端

#### 使用第三方服务

1.  [fullcontentrss](http://fullcontentrss.com/)  推荐指数：⭐️⭐️⭐️⭐️⭐️
3.  [Full-Text RSS](http://ftr.fivefilters.org/)    推荐指数：⭐️⭐️⭐️⭐️
4.  [freefullrss](https://www.freefullrss.com/)        推荐指数：⭐️⭐️⭐️

### 信息过滤

当RSS内容既包含你想要的内容，也有一些不想看到的内容，需要使用关键字过滤。

1. inoreader非付费用户只能过滤一个订阅源。
2. 如果需要大量过滤，可以尝试搭建**Tiny Tiny RSS**。

### 制作RSS Feed

#### 1：Feed43（免费）

官网：http://feed43.com/   

推荐指数：⭐️⭐️⭐️

教程：[FEED43新手教程：为任意网页定制RSS格式订阅源](https://post.smzdm.com/p/553684/)

#### 2：Fivefilters Feed Creator

官网：http://createfeed.fivefilters.org/index.php

推荐指数：⭐️⭐️⭐️⭐️

1. “Enter web page URL”就是输入网页网址，例如https://www.ipcfun.com/

2. “Look for links inside HTML elements whose id or class attribute contains” 根据ID或Class筛选元素，例如entry-title

3. “Only keep links if link URL contains”URL过滤，仅保留包含指定字符串的链接，例如html

   ![Fivefilters Feed Creator](/pic/rss-tutorial-3.jpg)

#### 3：Fetchrss

官网：http://fetchrss.com/ 

推荐指数：⭐️⭐️⭐️⭐️

GUI界面操作，非常简单易懂。

### inoreader使用体验提升

#### 安装去广告插件[AdBlock](https://chrome.google.com/webstore/detail/adblock-%E2%80%94-best-ad-blocker/gighmmpiobklfepjocnamgkkbiglidom)

此浏览器插件可以解决在使用免费版Inoreader阅读文章免除广告的骚扰

#### 安装油猴脚本：[显示防盗链图片 for Inoreader](https://greasyfork.org/zh-CN/scripts/376884-%E6%98%BE%E7%A4%BA%E9%98%B2%E7%9B%97%E9%93%BE%E5%9B%BE%E7%89%87-for-inoreader)

此脚本可以解决在Inoreader订阅爱稀奇时图片不能正常显示的问题

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

## 更新日志

- 2020-3-17：
1. 更新现在的使用方式
2. 重新排版，去除一些无用的内容，删除失效的工具
3. 添加新的RSS全文输出工具：rss2full
4. 解决Inoreader显示防链接图片问题

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