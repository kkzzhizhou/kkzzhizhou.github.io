---
title: Hexo+Next博客个性化配置
date: 2018-03-31 10:19:47
updated: 2018-7-7 19:23:28
tags: [Blog,静态博客]
---

## 使用的主题：NexT 

## 1. 全文搜索
### 添加百度/谷歌/本地 自定义站点内容搜索

安装`hexo-generator-searchdb`

```
npm install hexo-generator-searchdb --save
```

在站点的 _config.yml中增加

```
search:
  path: search.xml
  field: post
  format: html
  limit: 10000
```

## 2. 多平台同步
### 2.1 将本地博客同步到bitbucket上

原理很简单，将blog整个目录除了public文件夹之外的所有文件通过Git方式上传至bitbucket。

### 2.2 从bitbucket恢复数据

同理，恢复时只需要同步到数据即可。

## 3. 显示feed链接
打开主题的 `_config.yml` 中，将 `rss` 字段设置为：

1. `rss: false`，这将会禁用Feed链接。

2. `rss:`，当值为空的时候，默认会使用站点的 Feed 链接。在此之前需要使用 [hexo-generator-feed](https://github.com/hexojs/hexo-generator-feed) 插件生成 Feed。

   依照 `hexo-generator-feed` 插件的安装说明进行 Feed 生成，当配件配置完毕后，主题将自动显示 Feed 链接。

3. `rss: http://your-feed-url`，指定特定的链接地址，适用于已经烧制过 Feed 的情形。

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

<!-- more --> 

## 5. 修改标签样式

## 6. Fork me on github

## 7. 代码高亮

## 8. 顶部加载条

## 9. 文章阅读次数