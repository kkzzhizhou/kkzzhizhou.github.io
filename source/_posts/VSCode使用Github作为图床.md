---
title: VSCode使用Github作为图床
comments: true
date: 2020-04-05 12:47:00
updated: 2020-04-05 14:29:36
tags: 
- 图床
categories:
- Hexo
abbrlink: vscode-use-github-as-pic-bed
---

## 最终效果

使用VSCode插件PicGo上传图片至Github博客（比如kkzzhizho.github.io)的images分支。

## 博客仓库原先状态

一共有两个分支：source（博客源文件）和master（Hexo博客生成文件)

<!-- more --> 

## 实现步骤

### 新建一个远程空白分支：images

```
# 将项目克隆到本地
git clone xxx
cd xxx
# 新建一个空白images
git checkout --orphan images
# 清空当前项目
git rm -rf .
# 新建一个README.md文件（因为分支文件为空时不能推送到远端）
echo "This is a imgaes branch" > README>.md
# 提交到远端
git add -A
git commit -m "Initial images branch"
git push origin images
```

### 安装并配置VSCode插件：PicGo

1. 安装PicGo插件

需要用到Picgo这个插件，直接在vscode中搜索安装就行。

2. 配置PicGo插件

![vscode-use-github-as-pic-bed-1.png](https://raw.githubusercontent.com/kkzzhizhou/kkzzhizhou.github.io/images/vscode-use-github-as-pic-bed-1.png)

3. 申请Github Token

![vscode-use-github-as-pic-bed-2.png](https://raw.githubusercontent.com/kkzzhizhou/kkzzhizhou.github.io/images/vscode-use-github-as-pic-bed-2.png)

![vscode-use-github-as-pic-bed-3.png](https://raw.githubusercontent.com/kkzzhizhou/kkzzhizhou.github.io/images/vscode-use-github-as-pic-bed-3.png)

![vscode-use-github-as-pic-bed-4.png](https://raw.githubusercontent.com/kkzzhizhou/kkzzhizhou.github.io/images/vscode-use-github-as-pic-bed-4.png)

![vscode-use-github-as-pic-bed-5.png](https://raw.githubusercontent.com/kkzzhizhou/kkzzhizhou.github.io/images/vscode-use-github-as-pic-bed-5.png)