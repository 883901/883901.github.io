---
title: 将hexo源文件到分支
date: 2019-07-24 20:20:33
tags: hexo
categories: Next主题
---
hexo文件搭建好了之后，想到一个问题，如果博客出了什么问题怎么办，就想到把hexo源文件备份到github分支是最好的了.
<!-- more -->
## 解决方案
1.在github上建立一个仓库，然后把hexo文件夹上传，进行备份。

2.在现有的883901.github.io的repository创建一个分支来管理，具体操作如下：

### 一：建立分支hexo
#### 1.在本地D盘下（位置任意）右键Git bash here，执行以下指令，把883901.github.io项目文件克隆到本地：
```
git clone git@github.com:883901/883901.github.io.git
```
#### 2.然后D盘下就会有个883901.github.io的文件夹，里面的文件就是repository上的。
#### 3.进入883901.github.io，删除文件夹里除了.git的其他所有文件.
#### 4.把hexo原文件夹内的所有文件全部复制到883901.github.io/下.
#### 5.创建一个叫hexo（或者blog，名字随意）的分支，并切换到这个分支
```
git checkout -b hexo
```
#### 6.添加所有文件到暂存区
```
git add --all
```
#### 7.进行提交
```
git commit -m ""
```
#### 8.推送hexo分支的文件到github仓库
```
git push --set-upstream origin hexo
```

### 二、发布文章后更新hexo分支方法
#### 1.执行以下命令：
```
git add . #添加所有文件到暂存区
git commit -m "提交一篇博客"  #提交
git push origin hexo 推送hexo分支到github

git remote add origin git@github.com:883901/883901.github.io.git 
```
### 三、换电脑操作方案
#### 1.配置好基本的环境，npm install 安装依赖，然后克隆分支到本地
```
git clone -b hexo git@github.com:883901/883901.github.io.git
```

环境配置好了，hexo文件克隆到了本地，你就可以按照以前的步骤发博客了




