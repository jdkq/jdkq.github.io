---
title: 配置Vue-element-admin安装node-sass入坑
tags:
  - Vue
categories:
  - Vue
  - Vue-element-admin
cover: >-
  https://img1.baidu.com/it/u=3306102985,2313411151&fm=253&fmt=auto&app=138&f=PNG?w=2291&h=500
poster:
  topic: 由于npm编译失败的解决措施
  headline: 配置Vue-element-admin安装node-sass入坑日记
  caption: null
  color: black
abbrlink: e874c650
date: 2020-04-12 22:35:37
banner:
h1:
---
> 官方文档：https://panjiachen.github.io/vue-element-admin-site/zh/guide/#%E7%9B%AE%E5%BD%95%E7%BB%93%E6%9E%84

> 我在安装vue=element-admin的时候出现的错误

## 安装

```bash
# 克隆项目
git clone https://github.com/PanJiaChen/vue-element-admin.git

# 进入项目目录
cd vue-element-admin

# 安装依赖
npm install

# 建议不要用 cnpm 安装 会有各种诡异的bug 可以通过如下操作解决 npm 下载速度慢的问题
npm install --registry=https://registry.npm.taobao.org

# 本地开发 启动项目
npm run dev
```

在执行 `npm install` 安装package.json 依赖时出现如下`npm err`

```bash
> node-sass@4.13.1 install D:\Project\vue-admin-app\vue-element-admin\node_modules\node-sass
> node scripts/install.js

Downloading binary from https://github.com/sass/node-sass/releases/download/v4.13.1/win32-x64-72_binding.node
Cannot download "https://github.com/sass/node-sass/releases/download/v4.13.1/win32-x64-72_binding.node":

ESOCKETTIMEDOUT

Hint: If github.com is not accessible in your location
      try setting a proxy via HTTP_PROXY, e.g.

      export HTTP_PROXY=http://example.com:1234

or configure npm proxy via

      npm config set proxy http://example.com:8080

> node-sass@4.13.1 postinstall D:\Project\vue-admin-app\vue-element-admin\node_modules\node-sass
> node scripts/build.js

Building: C:\Program Files\nodejs\node.exe D:\Project\vue-admin-app\vue-element-admin\node_modules\node-gyp\bin\node-gyp.js rebuild --verbose --libsass_ext= --libsass_cflags= --libsass_ldflags= --libsass_library=
gyp info it worked if it ends with ok
gyp verb cli [
gyp verb cli   'C:\\Program Files\\nodejs\\node.exe',
gyp verb cli   'D:\\Project\\vue-admin-app\\vue-element-admin\\node_modules\\node-gyp\\bin\\node-gyp.js',
gyp verb cli   'rebuild',
gyp verb cli   '--verbose',
gyp verb cli   '--libsass_ext=',
gyp verb cli   '--libsass_cflags=',
gyp verb cli   '--libsass_ldflags=',
gyp verb cli   '--libsass_library='
gyp verb cli ]
gyp info using node-gyp@3.8.0
gyp info using node@12.16.2 | win32 | x64
gyp verb command rebuild []
gyp verb command clean []
gyp verb clean removing "build" directory
gyp verb command configure []
gyp verb check python checking for Python executable "python2" in the PATH
gyp verb `which` failed Error: not found: python2
gyp verb `which` failed     at getNotFoundError (D:\Project\vue-admin-app\vue-element-admin\node_modules\which\which.js:13:12)
gyp verb `which` failed     at F (D:\Project\vue-admin-app\vue-element-admin\node_modules\which\which.js:68:19)
gyp verb `which` failed     at E (D:\Project\vue-admin-app\vue-element-admin\node_modules\which\which.js:80:29)
gyp verb `which` failed     at D:\Project\vue-admin-app\vue-element-admin\node_modules\which\which.js:89:16
gyp verb `which` failed     at D:\Project\vue-admin-app\vue-element-admin\node_modules\isexe\index.js:42:5
gyp verb `which` failed     at D:\Project\vue-admin-app\vue-element-admin\node_modules\isexe\windows.js:36:5
gyp verb `which` failed     at FSReqCallback.oncomplete (fs.js:167:21)
gyp verb `which` failed  python2 Error: not found: python2
gyp verb `which` failed     at getNotFoundError (D:\Project\vue-admin-app\vue-element-admin\node_modules\which\which.js:13:12)
gyp verb `which` failed     at F (D:\Project\vue-admin-app\vue-element-admin\node_modules\which\which.js:68:19)
gyp verb `which` failed     at E (D:\Project\vue-admin-app\vue-element-admin\node_modules\which\which.js:80:29)
gyp verb `which` failed     at D:\Project\vue-admin-app\vue-element-admin\node_modules\which\which.js:89:16
gyp verb `which` failed     at D:\Project\vue-admin-app\vue-element-admin\node_modules\isexe\index.js:42:5
gyp verb `which` failed     at D:\Project\vue-admin-app\vue-element-admin\node_modules\isexe\windows.js:36:5
gyp verb `which` failed     at FSReqCallback.oncomplete (fs.js:167:21) {
gyp verb `which` failed   stack: 'Error: not found: python2\n' +
gyp verb `which` failed     '    at getNotFoundError (D:\\Project\\vue-admin-app\\vue-element-admin\\node_modules\\which\\which.js:13:12)\n' +
gyp verb `which` failed     '    at F (D:\\Project\\vue-admin-app\\vue-element-admin\\node_modules\\which\\which.js:68:19)\n' +
gyp verb `which` failed     '    at E (D:\\Project\\vue-admin-app\\vue-element-admin\\node_modules\\which\\which.js:80:29)\n' +
gyp verb `which` failed     '    at D:\\Project\\vue-admin-app\\vue-element-admin\\node_modules\\which\\which.js:89:16\n' +
gyp verb `which` failed     '    at D:\\Project\\vue-admin-app\\vue-element-admin\\node_modules\\isexe\\index.js:42:5\n' +
gyp verb `which` failed     '    at D:\\Project\\vue-admin-app\\vue-element-admin\\node_modules\\isexe\\windows.js:36:5\n' +
gyp verb `which` failed     '    at FSReqCallback.oncomplete (fs.js:167:21)',
gyp verb `which` failed   code: 'ENOENT'
gyp verb `which` failed }
gyp verb check python checking for Python executable "python" in the PATH
gyp verb `which` failed Error: not found: python
gyp verb `which` failed     at getNotFoundError (D:\Project\vue-admin-app\vue-element-admin\node_modules\which\which.js:13:12)
gyp verb `which` failed     at F (D:\Project\vue-admin-app\vue-element-admin\node_modules\which\which.js:68:19)
gyp verb `which` failed     at E (D:\Project\vue-admin-app\vue-element-admin\node_modules\which\which.js:80:29)
gyp verb `which` failed     at D:\Project\vue-admin-app\vue-element-admin\node_modules\which\which.js:89:16
gyp verb `which` failed     at D:\Project\vue-admin-app\vue-element-admin\node_modules\isexe\index.js:42:5
gyp verb `which` failed     at D:\Project\vue-admin-app\vue-element-admin\node_modules\isexe\windows.js:36:5
gyp verb `which` failed     at FSReqCallback.oncomplete (fs.js:167:21)
gyp verb `which` failed  python Error: not found: python
gyp verb `which` failed     at getNotFoundError (D:\Project\vue-admin-app\vue-element-admin\node_modules\which\which.js:13:12)
gyp verb `which` failed     at F (D:\Project\vue-admin-app\vue-element-admin\node_modules\which\which.js:68:19)
gyp verb `which` failed     at E (D:\Project\vue-admin-app\vue-element-admin\node_modules\which\which.js:80:29)
gyp verb `which` failed     at D:\Project\vue-admin-app\vue-element-admin\node_modules\which\which.js:89:16
gyp verb `which` failed     at D:\Project\vue-admin-app\vue-element-admin\node_modules\isexe\index.js:42:5
gyp verb `which` failed     at D:\Project\vue-admin-app\vue-element-admin\node_modules\isexe\windows.js:36:5
gyp verb `which` failed     at FSReqCallback.oncomplete (fs.js:167:21) {
gyp verb `which` failed   stack: 'Error: not found: python\n' +
gyp verb `which` failed     '    at getNotFoundError (D:\\Project\\vue-admin-app\\vue-element-admin\\node_modules\\which\\which.js:13:12)\n' +
gyp verb `which` failed     '    at F (D:\\Project\\vue-admin-app\\vue-element-admin\\node_modules\\which\\which.js:68:19)\n' +
gyp verb `which` failed     '    at E (D:\\Project\\vue-admin-app\\vue-element-admin\\node_modules\\which\\which.js:80:29)\n' +
gyp verb `which` failed     '    at D:\\Project\\vue-admin-app\\vue-element-admin\\node_modules\\which\\which.js:89:16\n' +
gyp verb `which` failed     '    at D:\\Project\\vue-admin-app\\vue-element-admin\\node_modules\\isexe\\index.js:42:5\n' +
gyp verb `which` failed     '    at D:\\Project\\vue-admin-app\\vue-element-admin\\node_modules\\isexe\\windows.js:36:5\n' +
gyp verb `which` failed     '    at FSReqCallback.oncomplete (fs.js:167:21)',
gyp verb `which` failed   code: 'ENOENT'
gyp verb `which` failed }
gyp verb could not find "python". checking python launcher
gyp verb could not find "python". guessing location
gyp verb ensuring that file exists: C:\Python27\python.exe
gyp ERR! configure error
gyp ERR! stack Error: Can't find Python executable "python", you can set the PYTHON env variable.
gyp ERR! stack     at PythonFinder.failNoPython (D:\Project\vue-admin-app\vue-element-admin\node_modules\node-gyp\lib\configure.js:484:19)
gyp ERR! stack     at PythonFinder.<anonymous> (D:\Project\vue-admin-app\vue-element-admin\node_modules\node-gyp\lib\configure.js:509:16)
gyp ERR! stack     at callback (D:\Project\vue-admin-app\vue-element-admin\node_modules\graceful-fs\polyfills.js:295:20)
gyp ERR! stack     at FSReqCallback.oncomplete (fs.js:167:21)
gyp ERR! System Windows_NT 10.0.17763
gyp ERR! command "C:\\Program Files\\nodejs\\node.exe" "D:\\Project\\vue-admin-app\\vue-element-admin\\node_modules\\node-gyp\\bin\\node-gyp.js" "rebuild" "--verbose" "--libsass_ext=" "--libsass_cflags=" "--libsass_ldflags=" "--libsass_library="
gyp ERR! cwd D:\Project\vue-admin-app\vue-element-admin\node_modules\node-sass
gyp ERR! node -v v12.16.2
gyp ERR! node-gyp -v v3.8.0
gyp ERR! not ok
Build failed with error code: 1
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@1.2.12 (node_modules\fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@1.2.12: wanted {"os":"darwin","arch":"any"} (current: {"os":"win32","arch":"x64"})

npm ERR! code ELIFECYCLE
npm ERR! errno 1
npm ERR! node-sass@4.13.1 postinstall: `node scripts/build.js`
npm ERR! Exit status 1
npm ERR!
npm ERR! Failed at the node-sass@4.13.1 postinstall script.
npm ERR! This is probably not a problem with npm. There is likely additional logging output above.

npm ERR! A complete log of this run can be found in:
npm ERR!     C:\Users\董\AppData\Roaming\npm-cache\_logs\2020-04-12T14_25_48_942Z-debug.log

```

## 解决办法

* 利用淘宝镜像安装node-sass
```bash
npm i node-sass --sass_binary_site=https://npm.taobao.org/mirrors/node-sass/
```

* 因为上一次npm失败，所以需要把已下载的东西重新编译一下
```bash
npm rebuild node-sass
```
* 之后开始安装其余的以来
```bash
npm install
npm run dev  # 启动项目
```

* 结果
```bash
$ npm run dev

> vue-element-admin@4.2.1 dev D:\Project\vue-admin-app\vue-element-admin
> vue-cli-service serve

 INFO  Starting development server...
 10% building 2/2 modules 0 activei ?wds?: Project is running at http://localhost:9527/
i ?wds?: webpack output is served from /
i ?wds?: Content not from webpack is served from D:\Project\vue-admin-app\vue-element-admin\public
i ?wds?: 404s will fallback to /index.html
 98% after emitting CopyPlugin DONE  Compiled successfully in 33840ms22:33:08

```

## 效果图
![vue-element-ui](https://ae01.alicdn.com/kf/H864ec65372ad4c479252fd9ba540aef2I.png)
