---
title: 使用Travis CI，同步跨平台写博客方案
author: zzz
date: 2019-4-9 21:37:28
update: 2019-4-9 21:37:34
tags: git应用,博客
abbrlink: 91c3f927
---

## Travis CI说明

新建Source分支用于存储源文件，Master分支用于存储生成的网站文件

## 全新的电脑写博客

- 下载安装[Git](https://git-scm.com/downloads)，[HexoClient](https://github.com/gaoyoubo/hexo-client/releases)，[Node.js](https://nodejs.org/zh-cn/download/)

- 运行Git Bash

- 添加Nodejs环境配置

  ```
  touch ~/.bash_profile
  vi ~/.bash_profile
  ```

- 添加以下内容到.bash_profile文件中，保存退出

  ```
  #! /bin/bash
  # 添加环境变量
  PATH=$PATH:/c/Program\ Files/nodejs
  ```

- 运行以下命令刷新环境变量

  ```
  source ~/.bash_profile
  ```

- 下载安装SourceTree并登录

  ```
  git clone -b source https://github.com/kkzzhizhou/kkzzhizhou.github.io
  ```

- 下载安装SourceTree并登录

- 打开本地仓库kkzzhizhou.github.io

- 修改后进行提交即可

## 已经配置的电脑写博客

强制拉取所有更新到本地，放弃所有本地修改

```
git fetch --all
git reset --hard origin/source
git pull
```

## SourceTree发布文章

- 暂存所有，填写Commit之后提交即可