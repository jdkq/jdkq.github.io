---
title: npm安装、更新与卸载
tags:
  - npm
categories:
  - Nodejs
  - npm
cover: >-
  https://img1.baidu.com/it/u=3306102985,2313411151&fm=253&fmt=auto&app=138&f=PNG?w=2291&h=500
poster:
  topic: 利用nodejs自带npm完成各node_modules插件安装(必看)
  headline: npm安装、更新与卸载
  caption: null
  color: black
abbrlink: aa8b35df
date: 2020-03-16 14:48:01
banner:
h1:
---
{% ablock npm v9.7.1 color:warning %}
	npm 为你和你的团队打开了连接整个 JavaScript 天才世界的一扇大门。它是世界上最大的软件注册表，每星期大约有 30 亿次的下载量，包含超过 600000 个 包（package） （即，代码模块）。来自各大洲的开源软件开发者使用 npm 互相分享和借鉴。包的结构使您能够轻松跟踪依赖项和版本。
{% endablock %}

## npm 由三个独立的部分组成：
* 网站
	* 是开发者查找包（package）、设置参数以及管理 npm 使用体验的主要途径。
* 注册表（registry）
	* 是一个巨大的数据库，保存了每个包（package）的信息。
* 命令行工具
	* 通过命令行或终端运行。开发者通过 CLI 与 npm 打交道


## 安装途径：
从　node.js 官网进行安装


## 安装过程
> window10系统

**百度搜索nodejs**
进入官网选择windows进行下载

>
> linux -就拿deepinOS来说
>
> 这里有三种方法

### 1. 官方途径：通过包管理器方式安装

* node8版本：

```bash
curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
sudo apt-get install -y nodejs
```

* node10版本：

```bash
curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
sudo apt-get install -y nodejs
```
参考官方教程,但是很奇怪，会报错，猜测deepin系统的原因。

### 2.通过源码编译安装

在node官网下载专区找到系统对应的版本，鼠标右键复制链接。打开deepin终端输入：

1. 下载node

```bash
wget https://nodejs.org/dist/v8.11.4/node-v8.11.4-linux-x64.tar.xz
```

2. 解压文件

```bash
tar -xvf node-v8.11.4-linux-x64.tar.xz
```
3. 切换并查看node所在路径

```bash
cd node-v8.11.4-linux-x64/bin
pwd

```

4. 查看node版本

```bash
node -v
```
5. 将node和npm设置为全局 （注意路径为上述第3部的路径）

```bash
sudo ln /home/ubuntu/node-v8.11.4-linux-x64/bin/node /usr/local/bin/node
sudo ln /home/ubuntu/node-v8.11.4-linux-x64/bin/npm /usr/local/bin/npm
pwd
```

这种方法配置的环境容易出问题，在安装http-server时依然报错。

### 3.使用自带的apt安装

* 安装node与npm
```bash
sudo apt install nodejs
sudo apt install npm
```
* 安装管理nodejs 本身工具，n模块
```bash
sudo npm install -g n
```
* 升级 node 到制定版本，后接版本号
```bash
sudo n latest //最新版本
sudo n stable //稳定版本
sudo n lts //长期支持版本
```
* 升级 npm 到最新版本
```bash
sudo npm install npm@latest -g
```

## 利用npm下载本地包

```bash
#下载
npm install <package_name> #自动创建一个node_modules目录
npm -v

#更新
cd <需要更新的路径根目录>
npm update <package_name>
    
#卸载
cd <需要卸载的路径根目录>
npm uninstall <package_name>
```

## 利用npm下载全局包
```bash
#下载
npm install -g <package_name>
#更新
npm update -g <package_name>
#卸载
npm uninstall -g <package_name>
```
## “全局包”跟“本地包”的区别：

* 全局包：下载到电脑本地，可应用于所有
* 本地包：只作用于本地根目录


> 就看npm不爽，下载速度死慢死慢，对不住!我没忍住，要斯文点，抱歉...
> 下面介绍一下npm跟cnpm

<!--more-->

## npm
* 允许用户从npm服务器下载别人编写的第三方包使用
* 允许用户从上述服务器下载并安装别人写的命令行程序到本地并且可以使用
* 允许用户将自己写的包或者命令行上传到上述的服务器供别人使用

## npm 命令

* `npm -v` 来测试是否成功安装
* 查看当前目录已安装插件： `npm list`
* 更新全部插件： `npm update [--save-dev]`
* 使用 npm 更新对应插件：`npm update <name> [-g] [--save-dev]`
* 使用 npm 卸载插件： `npm install <name> [-g] [--save-dev]`

## cnpm

* 淘宝团队做的国内镜像，因为npm的服务器位于国外可能会影响安装。淘宝镜像与官方同步频率目前为 10分钟 一次以保证尽量与官方服务同步
* 安装： 命令提示符执行`npm install cnpm -g --registry=https://registry.npm.taobao.org`<br>
[cnpm](/img/cnpm.png)
* `cnpm  -v` 看看是否安装成功

> 插一句（一本正经的bb）: npm下载真的慢，不是电脑的问题！

## 通过改变地址来使用淘宝镜像
* npm的默认地址是 `https://registry.npmjs.org/`
* 可以使用 `npm config get registry` 来查看npm仓库地址
* 可以用 `npm config set registry https://registry.npm.taobao.org` 来改变默认下载地址，达到可以不安装 `cnpm` 就能采用淘宝镜像的目的，然后使用上面的get命令查看是否成功。

## 另外
* `-g` :全局安装
* `-S` :相当于`npm install module_name --save` 写入`package.json` 的 `devDependencies`，这里面的插件只用于开发环境，不用于生产环境，比如 `babel` 、 `webpack打包` 插件就是开发时的需要，真正程序打包并不需要的一些插件
* `-D`:相当于 `npm install module_name --save-dev`，写入 `package.json` 的`devDependencies` , `devDependencies` 里面的插件只用于开发环境，不用于生产环境。比如一些babel编译功能的插件、webpack打包插件就是开发时候的需要，真正程序打包跑起来并不需要的一些插件。

> 为什么要保存在`package.json` 因为node_module包实在是太大了。用一个配置文件保存，只打包安装对应配置文件的插件，按需导入。



## npm err安装报错解决办法

```bash
npm ERR! code ETIMEDOUT
npm ERR! errno ETIMEDOUT
npm ERR! network request to https://registry.npmjs.org/hexo-deployer-git failed, reason: connect ETIMEDOUT 211.136.113.1:8080
npm ERR! network This is a problem related to network connectivity.
npm ERR! network In most cases you are behind a proxy or have bad network settings.
npm ERR! network
npm ERR! network If you are behind a proxy, please make sure that the
npm ERR! network 'proxy' config is set properly.  See: 'npm help config'
```
在执行npm install时出现以上错误，尝试了很多种方法，都没有解决，最后使用http://stackoverflow.com/questions/20397883/npm-doesnt-install-any-modules-network-socket-hangs-up 中的方法，成功解决问题。

> 解决办法：

1.先清除以前代理设置
```bash
npm config set proxy null
npm config set https-proxy null
```
2.重新设置
```bash
npm config set registry http://registry.cnpmjs.org/
```

3.npm install


## 问题2 
```bash
npm ERR! Unexpected end of JSON input while parsing near '...exo-fs","version":"0.'

npm ERR! A complete log of this run can be found in:
npm ERR!     C:\Users\董\AppData\Roaming\npm-cache\_logs\2020-05-15T14_41_43_153Z-debug.log

```

解决办法：  `npm cache clean --force`