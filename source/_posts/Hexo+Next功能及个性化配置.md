---
title: Hexo+Next功能及个性化配置
tags:
  - Hexo
  - Next
categories: []
abbrlink: e473457b
date: 2019-03-16 17:14:42
updated: 2018-03-31 10:19:47
---
##  [Travis CI持续集成](https://kkzzhizhou.github.io/2019/03/16/Hexo%E4%BD%BF%E7%94%A8Travis%20CI%E6%8C%81%E7%BB%AD%E9%9B%86%E6%88%90/)

## RSS Feed

- 安装插件`hexo-generator-feed`

  ```
  npm install hexo-generator-feed --save
  ```

- 修改站点配置

  ```
  # Extensions
  ## Plugins: http://hexo.io/plugins/
  #RSS订阅
  plugin:
  - hexo-generator-feed
  #Feed Atom
  feed:
  type: atom
  path: atom.xml
  limit: 20
  ```

- ### 修改主题配置，添加如下配置

  ```
  rss: /atom.xml
  ```

## 站内全文搜索

- 安装 `hexo-generator-searchdb`，在站点的根目录下执行以下命令：

  ```
  $ npm install hexo-generator-searchdb --save
  ```

- 编辑 站点配置文件，新增以下内容到任意位置：

  ```
  search:
    path: search.xml
    field: post
    format: html
    limit: 10000
  ```

- 编辑 主题配置文件，启用本地搜索功能：

  ```
  # Local search
  local_search:
    enable: true
  ```

## 文章按更新时间排序
### 要修改的内容

- `/node_modules/hexo-generator-index/index.js`

  ```
  order_by: '-date'
  ```

  修改为

  ```
  order_by: '-updated'
  ```

  这样的话就**只**按 Front-matter 中的`updated`排序了，因此所有文章的 Front-matter 中都必须要有`updated`，已发布的文章可以手动修改或者找方法批量将 `data`换成`updated`，对于将来的文章，只要做如下修改：

  - `/scaffolds/post.md`

  在`date`后加入一行

  ```
  updated: {{ date }}
  ```

## Hexo链接持久化

-  安装`hexo-abbrlink`这个插件

  ```
  npm install hexo-abbrlink --save
  ```

- 站点配置文件里:

  ```
  permalink: post/:abbrlink.html
  abbrlink:
    alg: crc32  # 算法：crc16(default) and crc32
    rep: hex    # 进制：dec(default) and hex
  ```

## <!-- more --> 