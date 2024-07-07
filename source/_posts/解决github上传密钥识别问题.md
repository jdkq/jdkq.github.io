---
title: 解决多个github上传密钥识别问题
tags:
  - git
categories:
  - git
  - Github本地多包上传
cover: >-
  https://img1.baidu.com/it/u=3306102985,2313411151&fm=253&fmt=auto&app=138&f=PNG?w=2291&h=500
poster:
  topic: 创建本体配置文件~/.ssh/touch config解决上传Host唯一性
  headline: 解决多个github上传密钥识别问题
  caption: null
  color: black
abbrlink: 884d0c65
date: 2020-08-31 20:28:29
banner:
h1:
---

# 小结： 此功能对于两个本地文件夹上传到两个不同github有利我才写的这篇博客

> 因为想要上传到github，做第二个主题博客遇到了些难题

* 申请一个新的邮箱(此处我想到了126网易笨邮箱)
* 创建一个新的github账号 (此处省略无数根头发)
* `vim ~/.ssh/id_rsa.pub` 在setting里设置ssh密钥
* 然后更改repo地址

<hr>

**很不幸此时上传出现了问题**

```
Error: Permission to xxx denied to xxx
```

*真是愁傻了人！！！！！！库里奥 于是 ↓*

> 百度程序员请战

**三种种解决方式**

1. 换台电脑继续配置密钥 [显然我没有钱]

2. 用虚拟机或者再在电脑上装双系统 [太浪费时间]

3. 设置两个密钥（也可以多个看你心情）

> 显然第三种方式可取

## 步骤1

**创建一个新的密钥**

**eg: 创建一个叫aysee的密钥**

```
ssh-keygen -t rsa -C "YOUR_EMAIL@YOUREMAIL.COM" -f ~/.ssh/aysee
cat ~/.ssh/aysee.pub
```
## 步骤2

* 新建仓库 

* 然后把显示出来的密钥粘贴到github 的setting SSH密钥里

## 步骤3

在电脑**~/.ssh/**里 `touch config` 一个配置文件让git_bash 能看出来谁上传的(Host)
> 我看出来了很多悲剧的发生
```bash
  #Default GitHub
  Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa

  #new github
  Host github-boreas6
  HostName github.com
  User git
  IdentityFile ~/.ssh/aysee
```

> 其中 `Host` 和 `IdentityFile` 非常重要 [笨机器识别就靠这玩意]


## 步骤4

* 修改主题配置根目录文件

`+++`: 仓库名
`×××××××××××`: 仓库地址

```bash
deploy:
  type: git
  repository: git@github-boreas6: +++/×××××××××××.git
  branch: master
```

注意： 这里的不是`github.com`而是`github-boreas6`上传到 github 的，对仓库有读写权的现在两位

> 完美！结束

```bash
Enumerating objects: 69, done.
Counting objects: 100% (69/69), done.
Delta compression using up to 4 threads
Compressing objects: 100% (49/49), done.
Writing objects: 100% (69/69), 348.86 KiB | 813.00 KiB/s, done.
Total 69 (delta 20), reused 0 (delta 0)
remote: Resolving deltas: 100% (20/20), done.
To github-boreas6:+++/×××××××××××.git
 * [new branch]      HEAD -> master
Branch 'master' set up to track remote branch 'master' from 'git@github-boreas6:+++/×××××××××××.git'.
INFO  Deploy done: git
```

# 总结

感觉把博客加上了吉他谱模块造成请求太多而卡顿于是另开一个博客

`链接我新的网抑云`: https://pdxwyy.github.io/

> 快来看看吧 ^-^ 