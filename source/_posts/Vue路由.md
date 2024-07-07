---
title: Vue路由
tags:
  - Vue
categories:
  - Vue
  - Vue路由
cover: >-
  https://img1.baidu.com/it/u=3306102985,2313411151&fm=253&fmt=auto&app=138&f=PNG?w=2291&h=500
poster:
  topic: 用于单页面链接切换、监听、方法执行
  headline: Vue路由
  caption: null
  color: black
abbrlink: 92619e7d
date: 2020-06-13 16:22:27
banner:
h1:
---
# 前端路由和后端路由的概念

* 后端路由： 对于普通网站，所有的链接都是URL地址，所有的URL地址都对应服务器上对应的资源

* 前端路由： 对于单页面应用程序来说，主要通过URL的hash(#号),来实现不同页面之间的切换，同时，hash有一个特点，HTTP请求中不包含hash相关的内容，所以单页面程序中的页面跳转主要用hash来实现

**在单页面应用程序中，这种通过hash改变切换页面的方式，称作`前端路由（区别于后端路由）`**

> [vue-router](https://router.vuejs.org/zh/)

# Vue-router3.0安装方式：

* 外引：https://unpkg.com/vue-router@3.0.0/dist/vue-router.js
```html
<script src="/path/to/vue.js"></script>
<script src="https://unpkg.com/vue-router@3.0.0/dist/vue-router.js"></script>
```

* webpack 打包
```bash
npm install vue-router
```

```javascript
import Vue from 'vue'
import VueRouter from 'vue-router'

Vue.use(VueRouter)
```

* 构建开发版
```bash
git clone https://github.com/vuejs/vue-router.git node_modules/vue-router
cd node_modules/vue-router
npm install
npm run build
```


# 基本用法
```html
		<div id="app">
			<!-- 地址 -->
			<p><font color="red">*</font>地址:<span>{{route_path}}</span></p>
			<font color="red">地址无刷新不会变化，这也正印证了上边的特性</font>

			<router-link to="/login">登录</router-link>
    		<router-link to="/register">注册</router-link><br>
			<router-view></router-view>
		</div>
		<template id="login">
			<div>
				<label>用户名</label>
				<input type="text" name=""><br>
				<label>密码</label>
				<input type="text" name=""><br>
				<button type="button">登录</button>
			</div>
		</template>
		<template id="register">
			<div>
				<label>用户名:</label>
				<input type="text" name=""><br>
				<label>密码:</label>
				<input type="text" name=""><br>
				<label>确认密码:</label>
				<input type="text" name=""><br>
				<button type="button">注册</button>				
			</div>

		</template>	
```
```javascript
			//创建一个路由对象，当导入vue-router包之后，在window 全局对象中就有了一个路由构造函数 vueRouter
			// 在new一个路由对象的时候，可以为构造函数，传递一个配置对象
			var login = {
				template:'#login'
			}
			var register = {
				template:'#register'
			}

			var routerObj = new VueRouter({
				routes:[
				// 每个路由规则，都是一个对象，这个规则对象身上有两个必须的属性
				// 1. path: 表示坚挺的路由链接地址
				// 2. component 表示如果匹配则展示对应组件(必须是组件模板对象而不是组件名称)
					{path:'/login',component:login},
					{path:'/register',component:register},
				] //表示路由匹配规则
			})
			var vm = new Vue({
				el:'#app',
				data:{
					route_path: ''
				},
				methods:{
				},
				created(){
					this.route_path = this.$route.path
				},
				components:{
					login,
					register
				},
				// 将路由规则对象，注册到vm实例上，用来监听URL地址的变化，然后展示对应的组件
				router:routerObj
			})
```



*这样默认展示根路径 `/`，很别扭*

```javascript
	var routerObj = new VueRouter({
		routes:[
		//表示路由匹配规则
		// 重定向 / 的 url地址 利用redirect 不属于Node里的redirect
		// 目的：手动修改哈希值
			{path:'/',redirect:'/login'}
			{path:'/login',component:login},
			{path:'/register',component:register},
		] 
	})
```


### 需求1：设置选中路由高亮
```html
	<style>
		.router-link-active{
			color:red;
			font-weight:800;
			font-style: italic;
			font-size:20px;
			text-decoration: underline;
			background-color:green;
		}
	</style>
```
```javascript
	var routerObj = new VueRouter({
		routes:[
		//表示路由匹配规则
		// 重定向 / 的 url地址 利用redirect 不属于Node里的redirect
		// 目的：手动修改哈希值
			{path:'/',redirect:'/login'}
			{path:'/login',component:login},
			{path:'/register',component:register},
		],
		linkActiveClass:'myactive'
	})
```


### 需求2: 为路由切换加入动画
```html
	<style>
		.v-enter,
		.v-leave{
			opacity: 0;
			transform: translateX(140px)
		}
		.v-enter-active,
		.v-leave-active{
			transition: all 0.4s ease
		}
	</style>
	<transition mode="out-in">
		<router-view></router-view>
	</transition>
```
<iframe src="/file/vue-router.html" width="100%" frameborder="0" height="400px"></iframe>

# 路由规则中定义参数 

* $route.query

```html
	<div id="app">
		<!-- 如果在路由中，使用传参，不需要修改path -->
		<router-link to="/login?id=1&name=dong">登录</router-link>
		<router-link to="/register">注册</router-link>
		<router-view></router-view>
	</div>
```
```javascript
			var login = {
				template:'<h1>登录---ID：{{$route.query.id}}---用户：{{$route.query.name}}</h1>',
				created(){
					console.log(this.$route)
				}
			}
			var register = {
				template:'<h1>注册</h1>'
			}
			var router = new VueRouter({
				routes:[
					{path:'/',redirect: '/login'},
					{path:'/login',component: login},
					{path:'/register',component: register}
				]
			})
			var vm = new Vue({
				el:'#app',
				data:{

				},
				methods:{},
				router:router
			})
```
<iframe src="/file/query传参.html" width="100%" frameborder="0" height="200px"></iframe>

* $route.params
```html
	<div id="app">
		<!-- 如果在路由中，使用传参，不需要修改path -->
		<router-link to="/login/:id">登录</router-link>
		<router-link to="/register">注册</router-link>
		<router-view></router-view>
	</div>
```
```javascript
			var login = {
				template:'<h1>登录---{{$route.params.id}}</h1>',
				created(){
					console.log(this.$route)
				}
			}
			var register = {
				template:'<h1>注册</h1>'
			}
			var router = new VueRouter({
				routes:[
					{path:'/',component: login},
					{path:'/login/12',component: login},
					{path:'/register',component: register}
				]
			})
			var vm = new Vue({
				el:'#app',
				data:{

				},
				methods:{},
				router:router
			})
```

# 路由的嵌套(children)

*使用 `children` 属性 ,实现子路由，同时，子路由的path前面，不要带 / ，否则永远以根路径开始请求，这样不方便用户理解 `url 地址`*
```html
		<div id="app">
			<router-link to="/account">Account</router-link>
			<router-view></router-view>
		</div>
		<template id="temp1">
			<div>
				<h1>这是Account组件</h1>
				<router-link to="/account/login">登录</router-link>
				<router-link to="/account/register">注册</router-link>
				<router-view></router-view>
			</div>
		</template>
```
```javascript
			var account = {
				template:'#temp1'
			}
			var login = {
				template:'<h4>登录</h4>'
			}
			var register = {
				template:'<h4>注册</h4>'
			}
			var router = new VueRouter({
				routes:[
					{	
						path:'/account',
						component:account,
						children:[
							{path:'login',component:login},
							{path:'register',component:register}	
						]
					}
					// {path:'/account/login',component:login},
					// {path:'/account/register',component:register}
				]
			})	
			var vm = new Vue({
				el:'#app',
				data:{},
				methods:{},
				router:router
			})
```
<iframe src="/file/children_router.html" width="100%" frameborder="0" height="400px"></iframe>

# 使用命名视图实现经典布局

```css
	<style type="text/css">
		html,body{
			margin: 0;
			padding: 0
		}
		h1{
			margin: 0;
			padding: 0;
			font-size: 16px
		}
		.header{
			height: 80px;
			background-color: orange
		}
		.container{
			display: flex;
			height: 600px;
		}
		.left{
			background-color: lightgreen;
			flex:2;
		}
		.main{
			background-color: lightpink;
			flex: 8
		}
```
```html
		<div id="app">
			<router-view></router-view>
			<div class="container">
				<router-view name="left"></router-view>
				<router-view name="main"></router-view>
			</div>
		</div>
		<template id="header">
			<div class="header">
				头部区域
			</div>
		</template>
		<template id="leftBox">
			<div class="left">
				左边区域
			</div>
		</template>
		<template id="MainBox">
			<div class="main">
				主区域
			</div>
		</template>
```
```javascript
		var header = {
			template:'#header'
		}
		var leftBox = {
			template:'#leftBox'
		}
		var MainBox = {
			template:'#MainBox'
		}
		var router = new VueRouter({
			routes:[
				// {path:'/',component: header},
				// {path:'/left',component: header},
				// {path:'/main',component: header},
				{
					path:'/',
					components:{
						'default': header,
						'left': leftBox,
						'main': MainBox
					}
				}
			]
		})
		var vm = new Vue({
			el:'#app',
			data:{
			},
			methods:{},
			router:router
		})
```
> [效果链接](/file/路由命名视图实现经典布局.html)

# 案例： keyup事件实现

## 方式1
```html
	<div id="app">
		<!-- 监听文本框数据改变拼接成fullname -->
		<input type="text" name="" v-model="firstname" @keyup="getFullName">+
		<input type="text" v-model="lastname" name="" @keyup="getFullName">
		<input type="text" v-model="fullname" name="">
	</div>
```
```javascript
		var vm = new Vue({
			el:'#app',
			data:{
				firstname:'',
				lastname:'',
				fullname:''
			},
			methods:{
				getFullName:function(){
					this.fullname = this.firstname+'-'+ this.lastname
				}
			},
		})
```
### 效果
<iframe src="/file/keyup名称案例.html" frameborder="0" width="100%" height="200px" scrolling="false"></iframe>

## 方式2
```html
	<div id="app">
		<!-- 监听文本框数据改变拼接成fullname -->
		<input type="text" name="" v-model="firstname">+
		<input type="text" v-model="lastname" name="">
		<input type="text" v-model="fullname" name="">
	</div>
```
```javascript
		var vm = new Vue({
			el:'#app',
			data:{
				firstname:'',
				lastname:'',
				fullname:''
			},
			methods:{
			},
			watch:{
				// 使用这个属性，可以监视watch data事件的变化，然后触发方法
				'firstname':function(newVal,oldValue){
					// this.fullname = this.firstname + '-' + this.lastname
					this.fullname = newVal + '-' + this.lastname
				},
				'lastname':function(newVal){
					this.fullname = this.firstname + '-' + newVal
				}
			}
		})
```
## 方式3
```html
	<div id="app">
		<!-- 监听文本框数据改变拼接成fullname -->
		<input type="text" name="" v-model="firstname">+
		<input type="text" v-model="lastname" name="">
		<input type="text" v-model="fullname" name="" readonly>
	</div>
```
```javascript
		var vm = new Vue({
			el:'#app',
			data:{
				firstname:'',
				lastname:'',
			},
			methods:{
			},
			computed:{
				// 在computed 中，可以定义一些属性，这些属性叫做【计算属性】
				// 本质是一个方法，计算的时候把名称直接当作属性来使用，并不会当作方法来调用
				// 注意1: 计算属性，在引用的时候，一定不要加{}去调用，直接把他当作普通属性去使用就好了
				// 注意2： 只要计算属性，这个function 内部，所用到的任何data的变化会 【重新计算】
				// 注意3： 计算属性求值结果会缓存，方便下次直接使用，如果计算属性方法中，所有来的任何数据没发生变化，则不会重新对计算求值
				'fullname': function(){
					return this.firstname + '-' + this.lastname
				}
			}
		})
```
# 通过 watch 监听路由变化
## 代码
```html
	<div id="app">
		<router-link to="/login">登录</router-link>
		<router-link to="/register">注册</router-link>
		<!-- 
			需求：监听路由改变做出反应
		 -->
		<router-view></router-view>
	</div>
```
```javascript
		const login = {
			template:'<h4>这是登录组件，这个组件是爸爸我开发的</h4>'
		}
		const register = {
			template:'<h4>这是注册组件，这个组件是某某开发的</h4>'
		}
		const router = new VueRouter({
			routes:[
				{path:'/',component:login},
				{path:'/login',component: login},
				{path:'/register',component: register}
			]
		})
		var vm = new Vue({
			el:'#app',
			data:{

			},
			methods:{},
			router:router,
			watch:{
				'$route.path':function(newVal,oldVal){
					// console.log(newVal+'-'+oldVal)
					if (newVal==="/login") {
						alert('欢迎进入登录页面^-^')
					}else if(newVal === '/register'){
						alert('欢迎进入注册页面^-^')
					}
				}
			}
		})
```
<iframe src="/file/watch监听router.html" frameborder="0" width="100%" height="350px" scrolling="false"></iframe>

# 总结

1. `computed`属性的结果会缓存，除非以来的响应式属性发生变化才会重新计算算，主要当作属性来用
2. `method` 方法表示一个具体的操作，主要书写业务逻辑
3. `watch` 一个对象，就是需要观察的表达式，主要用来监听某些特定数据的变化，，从而进行某些逻辑操作，可以视为 `computed` + `method`