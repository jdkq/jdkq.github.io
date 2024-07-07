---
title: ElementUI+Vue的配套使用
tags:
  - Vue
  - ElementUI
categories:
  - Vue
  - ElementUI
cover: >-
  https://img1.baidu.com/it/u=3306102985,2313411151&fm=253&fmt=auto&app=138&f=PNG?w=2291&h=500
poster:
  topic: webpack的安装以及配合vue脚手架依赖安装
  headline: ElementUI+Vue的配套使用
  caption: null
  color: black
abbrlink: 67ef95a
date: 2020-09-06 23:52:00
banner:
h1:
---

> 基于webpack的element-ui组件 && vue
# 搭建开发环境
<hr>

## 1.安装webpack
```bash
npm install -g webpack
```

## 2.安装vue-cli

`vue-cli`： 是vue.js的脚手架，用于自动生成vue.js模板工程

使用步骤： 
* 安装vue-cli
```bash
npm install -g vue-cli
```

* 使用vue-cli构建项目
```bash
vue init webpack project-name //创建一个基于webpack模板的名叫project-name的项目
```

* 安装项目依赖
```bash
cd project-name
npm install
npm run dev
```
此时在浏览器打开： `localhost:8080`就可以看到对应的页面

* 但这个时候只能在本地跑，如果在服务器上访问 此时需要执行

```bash
npm run build
```

## 3.安装element-ui
```bash
npm i element-ui@next -D
```

## 4.开始使用
> 接下来就可以参照`Element-UI`的[官方文档](http://element.eleme.io/#/component/)上手开发了

**main.js**

* 完整引入
```javascript
// 在引入 Element 时，可以传入一个全局配置对象。该对象目前支持 size 与 zIndex 字段。size 用于改变组件的默认尺寸，zIndex 设置弹框的初始 z-index（默认值：2000）。按照引入 Element 的方式，具体操作如下：
import Vue from 'vue';
import Element from 'element-ui';
Vue.use(Element, { size: 'small', zIndex: 3000 });
```

* 按需引入
```bash
 # 按需求引入
 # 首先，安装 babel-plugin-component
npm install babel-plugin-component -D
```

将 `.babelrc` 修改成这个
```
{
  "presets": [["es2015", { "modules": false }]],
  "plugins": [
    [
      "component",
      {
        "libraryName": "element-ui",
        "styleLibraryName": "theme-chalk"
      }
    ]
  ]
}
```
npm run dev出现问题 `Module build failed: Error: Couldn't find preset "es2015" relative to directory`
```bash
Module build failed: Error: Couldn't find preset "es2015" relative to
directory "C:\\Users\\董\\Desktop\\project-name"
    at C:\Users\董\Desktop\project-name\node_modules\babel-core\lib\transformation\file\options\option-manager.js:293:19
    at Array.map (<anonymous>)
    at OptionManager.resolvePresets (C:\Users\董\Desktop\project-name\node_modules\babel-core\lib\transformation\file\options\option-manager.js:275:20)
    at OptionManager.mergePresets (C:\Users\董\Desktop\project-name\node_modules\babel-core\lib\transformation\file\options\option-manager.js:264:10)
    at OptionManager.mergeOptions (C:\Users\董\Desktop\project-name\node_modules\babel-core\lib\transformation\file\options\option-manager.js:249:14)
    at OptionManager.init (C:\Users\董\Desktop\project-name\node_modules\babel-core\lib\transformation\file\options\option-manager.js:368:12)
    at File.initOptions (C:\Users\董\Desktop\project-name\node_modules\babel-core\lib\transformation\file\index.js:212:65)
    at new File (C:\Users\董\Desktop\project-name\node_modules\babel-core\lib\transformation\file\index.js:135:24)
    at Pipeline.transform (C:\Users\董\Desktop\project-name\node_modules\babel-core\lib\transformation\pipeline.js:46:16)
    at transpile (C:\Users\董\Desktop\project-name\node_modules\babel-loader\lib\index.js:50:20)
    at Object.module.exports (C:\Users\董\Desktop\project-name\node_modules\babel-loader\lib\index.js:173:20)
```
* 解决方案
```bash
npm install --save-dev babel-preset-es2015
```

* 完整引入方式
```javascript
import Vue from 'vue';
import {
  Pagination,
  Dialog,
  Autocomplete,
  Dropdown,
  DropdownMenu,
  DropdownItem,
  Menu,
  Submenu,
  MenuItem,
  MenuItemGroup,
  Input,
  InputNumber,
  Radio,
  RadioGroup,
  RadioButton,
  Checkbox,
  CheckboxButton,
  CheckboxGroup,
  Switch,
  Select,
  Option,
  OptionGroup,
  Button,
  ButtonGroup,
  Table,
  TableColumn,
  DatePicker,
  TimeSelect,
  TimePicker,
  Popover,
  Tooltip,
  Breadcrumb,
  BreadcrumbItem,
  Form,
  FormItem,
  Tabs,
  TabPane,
  Tag,
  Tree,
  Alert,
  Slider,
  Icon,
  Row,
  Col,
  Upload,
  Progress,
  Spinner,
  Badge,
  Card,
  Rate,
  Steps,
  Step,
  Carousel,
  CarouselItem,
  Collapse,
  CollapseItem,
  Cascader,
  ColorPicker,
  Transfer,
  Container,
  Header,
  Aside,
  Main,
  Footer,
  Timeline,
  TimelineItem,
  Link,
  Divider,
  Image,
  Calendar,
  Backtop,
  PageHeader,
  CascaderPanel,
  Loading,
  MessageBox,
  Message,
  Notification
} from 'element-ui';

Vue.use(Pagination);
Vue.use(Dialog);
Vue.use(Autocomplete);
Vue.use(Dropdown);
Vue.use(DropdownMenu);
Vue.use(DropdownItem);
Vue.use(Menu);
Vue.use(Submenu);
Vue.use(MenuItem);
Vue.use(MenuItemGroup);
Vue.use(Input);
Vue.use(InputNumber);
Vue.use(Radio);
Vue.use(RadioGroup);
Vue.use(RadioButton);
Vue.use(Checkbox);
Vue.use(CheckboxButton);
Vue.use(CheckboxGroup);
Vue.use(Switch);
Vue.use(Select);
Vue.use(Option);
Vue.use(OptionGroup);
Vue.use(Button);
Vue.use(ButtonGroup);
Vue.use(Table);
Vue.use(TableColumn);
Vue.use(DatePicker);
Vue.use(TimeSelect);
Vue.use(TimePicker);
Vue.use(Popover);
Vue.use(Tooltip);
Vue.use(Breadcrumb);
Vue.use(BreadcrumbItem);
Vue.use(Form);
Vue.use(FormItem);
Vue.use(Tabs);
Vue.use(TabPane);
Vue.use(Tag);
Vue.use(Tree);
Vue.use(Alert);
Vue.use(Slider);
Vue.use(Icon);
Vue.use(Row);
Vue.use(Col);
Vue.use(Upload);
Vue.use(Progress);
Vue.use(Spinner);
Vue.use(Badge);
Vue.use(Card);
Vue.use(Rate);
Vue.use(Steps);
Vue.use(Step);
Vue.use(Carousel);
Vue.use(CarouselItem);
Vue.use(Collapse);
Vue.use(CollapseItem);
Vue.use(Cascader);
Vue.use(ColorPicker);
Vue.use(Transfer);
Vue.use(Container);
Vue.use(Header);
Vue.use(Aside);
Vue.use(Main);
Vue.use(Footer);
Vue.use(Timeline);
Vue.use(TimelineItem);
Vue.use(Link);
Vue.use(Divider);
Vue.use(Image);
Vue.use(Calendar);
Vue.use(Backtop);
Vue.use(PageHeader);
Vue.use(CascaderPanel);

Vue.use(Loading.directive);

Vue.prototype.$loading = Loading.service;
Vue.prototype.$msgbox = MessageBox;
Vue.prototype.$alert = MessageBox.alert;
Vue.prototype.$confirm = MessageBox.confirm;
Vue.prototype.$prompt = MessageBox.prompt;
Vue.prototype.$notify = Notification;
Vue.prototype.$message = Message;
```
## 5.例子

* App.vue
```HTML
<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h1>{{ msg }}</h1>
    <el-button @click.native="startHacking">Let's do it</el-button>
    <div class="block">
      <span class="demonstration">显示默认颜色</span>
      <span class="wrapper">
      <el-button type="success">成功按钮</el-button>
      <el-button type="warning">警告按钮</el-button>
      <el-button type="danger">危险按钮</el-button>
      <el-button type="info">信息按钮</el-button>
      </span>
    </div>
    <br/>
    <div class="block">
      <span class="demonstration">hover 显示颜色</span>
      <span class="wrapper">
        <el-button :plain="true" type="success">成功按钮</el-button>
        <el-button :plain="true" type="warning">警告按钮</el-button>
        <el-button :plain="true" type="danger">危险按钮</el-button>
        <el-button :plain="true" type="info">信息按钮</el-button>
      </span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data(){
    return{
      msg:'我开始用element了'
    }
  },
  methods:{
    startHacking(){
      this.$notify({
        title: '我上班了',
        message: '真好！又开始秃头了',
        duration: 6000
      })
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
body {
  font-family: Helvetica, sans-serif;
}
</style>
```

* main.js
```javascript
// The Vue build version to load with the `import` command
// (runtime-only or standalone) has been set in webpack.base.conf with an alias.
import Vue from 'vue'
import router from './router'
// import ElementUI from 'element-ui'
import {Button,Notification} from 'element-ui'
import 'element-ui/lib/theme-chalk/index.css'
import App from './App' 
Vue.config.productionTip = false
// 引入组件并且设置默认组件默认尺寸为small 弹框初始值为z-index=3000
// Vue.use(ElementUI,{size:'small',zIndex:3000})
Vue.use(Button)
Vue.prototype.$notify = Notification

/* eslint-disable no-new */
new Vue({
  el: '#app',
  router,
  components: { App },
  template: '<App/>'
})
```