---
title: Hexo+Next功能及个性化配置
tags: [Hexo,Next]
categories: []
date: 2019-03-16 17:14:42
create: 2018-03-31 10:19:47
---
## 1. RSS Feed
### 添加百度/谷歌/本地 自定义站点内容搜索

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

## 2. [Travis CI持续集成](https://kkzzhizhou.github.io/2019/03/16/Hexo%E4%BD%BF%E7%94%A8Travis%20CI%E6%8C%81%E7%BB%AD%E9%9B%86%E6%88%90/)

## 3. 全文搜索
## 4. 文章按更新时间排序
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

## 5. 修改标签样式

## 6. Fork me on github

## 7. 代码高亮

## 8. 顶部加载条

## 9. 文章阅读次数

......
<!-- more --> 