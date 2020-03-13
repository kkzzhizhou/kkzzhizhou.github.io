---
title: 使用OneDrive实时同步Ditto剪贴板数据（WebDav）
date: 2019-4-30 15:41:29
updated: 2019-4-30 15:41:32
tags: 跨设备工作
---

最近将常用的绿色软件放到Onedrive中同步，方便在自己的多个Windows设备使用。遇到一个比较棘手的问题，使用Ditto时会锁定数据库文件，此时OneDrive显示文件在使用中，无法同步。

解决方法：使用WebDav连接OneDrive

OneDrive使用WebDav的方法：

1. 访问 [OneDrive.com](http://onedrive.com/) ，点击进入任何一个你的文件夹。
2. 看浏览器上面的地址栏，“cid”后面的一串完整的数字加大写的英文字母叫 special ID（如下图）。
3. 你的入口链接就是： special ID（如我的就是https://d.docs.live.net/F399A8134684152B），账号密码就是你微软账号的账号密码
   - 如果你有**开启两步验证**功能，那么需要在[这里去获得一个生成的应用密码](https://account.live.com/proofs/AppPassword?mkt=en-us)
   - 另外要注意的，OneDrive 的 WebDav 接口如同坚果云的一样，传输的文件大小限制在100M以下。
4. 在资源管理器界面中，选择映射网络驱动器，在文件夹一栏，填入上一步得到的地址，点击完成，耐心等候，输入账号密码即可，之后可以将这个映射得到的盘符当作本地磁盘进行使用

连接后如下图所示，打开即为你网盘的文件

![](/pic/d22ff2eegy1g2kpigh93sj20ed051mx7.jpg)

Ditto设置如下图所示，数据库使用WebDav路径即可完美解决数据同步问题

![](/pic/d22ff2eegy1g2kpnvgzmpj20ic02t3yf.jpg)