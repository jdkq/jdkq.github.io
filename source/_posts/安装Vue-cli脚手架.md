---
title: 安装Vue-cli脚手架
tags:
  - Linux安装Vue-cli
categories:
  - Vue
  - 运行环境安装
cover: >-
  https://img1.baidu.com/it/u=3306102985,2313411151&fm=253&fmt=auto&app=138&f=PNG?w=2291&h=500
poster:
  topic: npm小妙招
  headline: 在Deepin操作系统安装Vue-cli
  caption: null
  color: black
abbrlink: e52449ab
date: 2020-04-20 14:08:38
banner:
h1:
---

> 我在使用deepin安装vue-cli时出现以下几个问题

1. 在用过 `npm install -g @vue-cli` 时：出现

![vue-cli安装错误1](https://ae01.alicdn.com/kf/Hecb582f01e384d7e885102af76f94caeG.png)

起初我以为安装中途结束，因为一只猫突然跳上我的笔记本键盘
然后又重新输入一遍但还是报上述图所示的问题

2. `npm cache clean --force` 清理缓存后决定再试一遍

![vue-cli安装错误2](https://ae01.alicdn.com/kf/H1b5f7923a65442fbb744fc3c9acb5e8fY.png)
然后我就懵了，入坑中...
猜测是不是因为权限问题，以及npm版本问题考虑，果断的使用cnpm安装vue-cli


3. `sudo npm install cnpm -g --registry=https://registry.npm.taobao.org` 之后再使用 `sudo cnpm install -g @vue-cli`来下载vue-cli脚手架

![cnpm安装vue_cli脚手架](https://ae01.alicdn.com/kf/Had5aaa407cea4fad9eca51a52a8ca336v.png)


4. 安装成功！开始上项目
