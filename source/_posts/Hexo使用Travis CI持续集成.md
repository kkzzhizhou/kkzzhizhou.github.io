---
title: Hexo使用Travis CI持续集成
date: 2019-03-16 16:23:44
create: 2019-03-16 16:23:44
tags: [Travis CI,Hexo]

---

## 使用CI之前:

- 使用命令行安装hexo环境
- 还需要敲几个命令：`hexo clean && hexo g && hexo d`

## 使用CI之后

- 使用HexoClient直接编辑一键发布

## CI 为何物

> CI（Continuous Integration）—— 持续集成。

其实光从名字其实能大致知道CI做了什么事情。硬件领域有集成模块、集成电路，软件领域也有集成概念：项目构建、自动化测试、部署等等。我的理解，每个成熟的产品从零散到成型到出品（上线）的过程，就是集成（Integration）。那么CI做的事情，就是让这个工程自动化，持续进行（Continuous）。

## Travis CI 又为何物

> Travis CI: 在线托管的CI服务，对开源项目是免费的。(仅适用有公开仓库)
>
> *travis*-*ci*.org只支持github上的公有仓库，而*travis*-*ci*.com则支持*私有仓库(需付费,价格不低)*。

## 如何配置Travis CI

### 1.GitHub账号直接登录

打开[Travis CI](https://travis-ci.org/) ,使用 GitHub 第三方授权登录。

### 2. 打开[链接](https://travis-ci.org/account/repositories)

- 勾上你的blog repo (这里我勾上了`kkzzhizhou.github.io`)，点击小齿轮，进入配置页。

![image-20190316163339901](https://ws3.sinaimg.cn/large/006tKfTcly1g14pz0ojjpj30t40j80ul.jpg)



### 3. 获取Pesonal Access Token

- 在GitHub个人账户 `Setting/ Developer settings/ Personal access tokens`下，新建一个Token，然后在Travis CI配置中，Environment Variables，添加生成的Token。

权限配置如下图所示:

![img](https://ws1.sinaimg.cn/large/006tKfTcgy1g14q5m1lyrj30sc0cl0up.jpg)

### 4. 参考我本页面的配置

- **CI_TOKEN的值为上步获得的Token**

![image-20190316163717457](https://ws4.sinaimg.cn/large/006tKfTcgy1g14q2myqp8j31h30ni77d.jpg)

### 5. 新建Source分支

```
git clone https://github.com/kkzzhizhou/kkzzhizhou.github.io //换成你自己的博客仓库
git checkout source //新建source分支,保留如下图所示的源文件
```

![image-20190316165017295](https://ws2.sinaimg.cn/large/006tKfTcgy1g14qg5wp5vj30dy061t9c.jpg)



### 6. Source分支下新建.travis.yml文件

```
language: node_js
node_js: stable
cache:
  directories:
    - node_modules

# S: Build Lifecycle
install:
  - npm install


#before_script:
 # - npm install -g gulp

script:
  - hexo clean && hexo g

after_script:
  - git clone https://${GH_REF} .deploy_git
  - cd .deploy_git
  - git checkout master
  - cd ../
  - mv .deploy_git/.git/ ./public/
  - cd ./public
  - git init
  - git config user.name "zzz" //修改成你自己的用户名
  - git config user.email "806508401@qq.com" //修改成你自己的邮箱
  - git add .
  - git commit -m ":memo:Update by Travis CI"
  - git push --force --quiet "https://${CI_TOKEN}@${GH_REF}" master:master
# E: Build LifeCycle

branches:
  only:
    - source
env:
 global:
   - GH_REF: github.com/kkzzhizhou/kkzzhizhou.github.io.git //修改成你自己的仓库
```

### 7. 上传至Source分支

```
git add .
git commit -m "hexo-source-upload"
git push origin source //推送到远程仓库
```

### 8. 使用HexoClient愉快写Blog了

![image.png](https://ws3.sinaimg.cn/large/006tKfTcgy1g14qmvlh1oj31cx0u011z.jpg)

......
<!-- more --> 

## 参考文章:

1. [Travis CI助力Blog持续输出](https://palmer.arkstack.cn/2018/01/Travis%20CI%E5%8A%A9%E5%8A%9BBlog%E6%8C%81%E7%BB%AD%E8%BE%93%E5%87%BA/)

2. [HexoClient使用帮助](https://www.mspring.org/2018/11/29/HexoClient%E4%BD%BF%E7%94%A8%E5%B8%AE%E5%8A%A9/)

3. [Travis-CI初体验](https://www.jianshu.com/p/157d15b388c9)