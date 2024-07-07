---
title: git提交文件篇
tags:
  - git
categories:
  - git
  - 利用gitbash提交文件到仓库
cover: >-
  https://img1.baidu.com/it/u=3306102985,2313411151&fm=253&fmt=auto&app=138&f=PNG?w=2291&h=500
poster:
  topic: 建立SSH信任后的仓库code代码提交方法
  headline: git向仓库提交文件
  caption: null
  color: black
abbrlink: 870bc40
date: 2020-03-12 11:17:36
banner:
h1:
---
{% quot 向服务器仓库提交文件  %}
 
## 1.创建描述文档

```bash
    touch README.md
```
## 2.添加文件
```bash
    git add 文件名
    git add . 一键add
```
## 3.提交文件
```bash
    git commit -m “提交文件说明”
    git remote add origin git@xx.xx.xx.xx:repos/xxx/xxx/xxx.git
```
## 4.推送到远程仓库
* 普通推送：
```bash
    git push 
```
* 强行推送：
```bash
    git push -u origin master
```

> 注意如果这一步报错就说明README.md文件没在本地，需要合并一下
```bash
git pull --rebase origin master
```