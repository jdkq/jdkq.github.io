---
title: vue组件
tags:
  - Vue
categories:
  - Vue
  - Vue组件
cover: >-
  https://img1.baidu.com/it/u=3306102985,2313411151&fm=253&fmt=auto&app=138&f=PNG?w=2291&h=500
poster:
  topic: 定义组件（私有标签）用于列表、数据切换、方法执行
  headline: Vue组件
  caption: null
  color: black
abbrlink: dd3b78a2
date: 2020-06-01 15:51:02
banner:
h1:
---
# 定义vue组件

* 组件：为了拆分vue实例的代码量，让我们不同的组件划分不同的功能模块，将来我们要什么样的功能直接调用组件即可！

* 组件化和模块化的不同：

	* 模块化：是从代码逻辑进行划分，方便代码分层开发，保证每个功能模块的只职能单一

	* 组件化： 是从UI界面角度进行划分的，前端的组件化方便UI组件的重用

# 创建全局组件

* 第一种方式
```javascript
		// 第一种
		// 使用Vue.extend 来创建全局vue组件
		var com1 = Vue.extend({
			template:'<h3>这是使用Vue.extend创建的组件</h3>'
				//通过template 属性。指定组件要展示的HTML结构

		})
		// 使用Vue.component('组件名称'，创建出来的组件模板对象)
		// 如果使用Vue.component定义全局组件的时候，组件名使用了驼峰命名，则在引用组件的时候，需要把大学的驼峰改成小写字母，同时用 '-'连接
		// 如果不是，直接拿名称命名就行
		Vue.component('myCom1',com1)
```
* 第二种方式

```javascript
		// 第二种
		// 组件模板必须有且只有一个唯一的根元素
		Vue.component('myCom2',{
			template:'<div><h3>这是使用Vue.component创建的组件</h3></div>'
		})
```
* 第三种方式

```html
	<div id="app">
		<my-com3></my-com3>
	</div>
	<template id="tmp1">
		<div>
			<h1>这是通过template 元素在外部定义的组件元素，这个方式，有代码的指示提示和高亮</h1>
			<h4>好用，不错！</h4>
		</div>
	</template>
```
```javascript
		// 第三种
		Vue.component('myCom3',{
			template:'#tmp1'
		})
		var vm = new Vue({
			el:'#app',
			data:{

			},
			methods:{},
		})
```

## 使用vue实例的render方法渲染组件(替换app里所有内容)
```html
	<div id="app">	

	</div>
```
```javascript
var login = {
	template: '<h1>登录组件</h1>'
}
var vm = new Vue({
	el:'#app',
	data:{},
	methods:{},
	render: function(createElements){
		// createElements 是一个方法，调用它，能够把指定的组件模板渲染为html结构
		return createElements(login)
		// 主题：这里return结果会自然替换el指定的容器
	}
})
```

# 创建组件使用`components`定义私有组

```html
	<div id="app-2">
		<login></login>
	</div>
	<template id="login">
		<div>				
			<label>用户名：</label><input type="text" name=""><br><label>密码：</label><input type="text" name=""><br><button type="button">登录</button>
		</div>
	</template>
```
```javascript
		var vm2 = new Vue({
			el:'#app-2',
			data:{},
			methods:{},
			directives:{},
			components:{
				login:{
					template:'#login'
				}
			},
			filters:{}
		})
```


# 组件中的data

## 注册一个定时器组件案例
*拿计时器案例讲：如果按照全局组件声明一个对象dataObj,`count`的值会相互影响，导致同一值*
```javascript
		var dataObj ={count:0}
		Vue.component('counter',{
			template: '#tmp_count',
			data: function(){
				return dataObj
			}
			methods:{
				increament:function(){
					this.count++	
				}
			}
		})	
```
### 结果
![外部声明data对象count值相互影响](https://ae01.alicdn.com/kf/H8906bd47f3414b8586e18a8c7cb0fd78K.jpg)


## 正确定义方法
```html
	<div id="app">
		<counter></counter>
		<counter></counter>
		<counter></counter>
	</div>
	<template id="tmp_count">
		<div>
			<input type="button" name="" value="+1" @click="increament">
			<h3>{{count}}</h3>
		</div>
	</template>
```
```javascript			
		// 注册一个计数器组件counter，每当点击data值里的count+1
		Vue.component('counter',{
			template: '#tmp_count',
			data: function(){
				return{
					count:0
				}
			},
			methods:{
				increament:function(){
					this.count++	
				}
			}
		})	
```
### 结果
![component内部声明data对象count值单一](https://ae01.alicdn.com/kf/H173b003148ed49c1be9a4734714dcecbU.jpg)
### 演示
<iframe src="/file/counter计数器.html" scrolling="false" width="100%" height="300px" frameborder="0"></iframe>


# 实现不同组件的切换

## 利用v-if & v-else 实现注册和登录切换
```html
	<div id="app">
		<a href="" @click.prevent="flag=true">登录</a>
		<a href="" @click.prevent="flag=false">注册</a>
		<login v-if="flag"></login>
		<register v-else="flag"></register>
	</div>
	<template id="login">
		<div>				
			<label>用户名：</label><input type="text" name=""><br><label>密码：</label><input type="text" name=""><br><button type="button">登录</button>
		</div>
	</template>
	<template id="register">
		<div>
			<label>用户名：</label><input type="text" name=""><br><label>密码：</label><input type="text" name=""><br><label>确认密码：</label><input type="text" name=""><br><button type="button">注册</button>
		</div>
	</template>
```
```javascript
		// 登录注册组件切换
		Vue.component('login',{
			template:'#login'
		})
		Vue.component('register',{
			template:'#register'
		})
		var vm = new Vue({
			el:'#app',
			data:{
				flag:true
			},
			methods:{}
		})
```
### 效果演示

<iframe src="/file/component_login_v-if_v-else.html" scrolling="false" width="100%" height="300px" frameborder="0"></iframe>

## 利用vue提供的component 实现组件切换

```html
	<div id="app">
		<!-- Vue 提供了component，来展示对应的名称组件 -->
		<!-- component 是一个占位符 :is 属性，可以用来指定要展示的组件名称 -->
		<a href="" @click.prevent="component_name='login'">登录</a>
		<a href="" @click.prevent="component_name='register'">注册</a>

		<component :is="component_name"></component>
		
	</div>
	<template id="login">
		<div>				
			<label>用户名：</label><input type="text" name=""><br><label>密码：</label><input type="text" name=""><br><button type="button">登录</button>
		</div>
	</template>
	<template id="register">
		<div>
			<label>用户名：</label><input type="text" name=""><br><label>密码：</label><input type="text" name=""><br><label>确认密码：</label><input type="text" name=""><br><button type="button">注册</button>
		</div>
	</template>
```
```javascript
		// 登录注册组件切换
		// 组件名称是字符串
		Vue.component('login',{
			template:'#login'
		})
		Vue.component('register',{
			template:'#register'
		})
		var vm = new Vue({
			el:'#app',
			data:{
				component_name: 'login'
			}
		})
```
*结果与第一种完全相同*


## 总结

*目前，当前学习了几个vue提供的标签*
`component`,`template`,`transition`



# 组件动画过度

```html
<style>
	.v-enter,
	.v-leave{
		opacity:0;
		transform: translateX(150px);
	}
	.v-enter-active,
	.v-leave-active{
		transition:all 0.5s ease
	}
</style>

<!-- 通过 mode 属性，设置组件切换模式 -->
<transition mode="out-in">
	<component :is="component_name"></component>
</transition>
```

## 演示：
<iframe src="/file/component_login_r.html" scrolling="false" width="100%" height="200px" frameborder="0"></iframe>

# 父组件向子组件传值或方法

* 传值【案例：com1】： 通过定义props属性绑定
* 传方法【案例：com2】：this.$emit('组件定义的方法',option)

```html
	<div id="app">
		<!-- 父组件可以在引用子组件的时候，通过属性绑定(:)的形式 ,把咱们需要传递给子组件的数据，以属性绑定的形式，传递到子组件内部，供子组件使用-->
		<com1 :parentmsg="msg"></com1>
		<!-- 父组件向子组件传递方法 -->
		<com2 @func="show"></com2>
	</div>
	<template id="tmp1">
		<div>
			<h3>这是一个子组件</h3>
			<button type="button"  @click="myclick">这是一个子组件按钮，点击触发父组件传递来的func方法</button>
		</div>
	</template>
```
```javascript
	var com2 = Vue.component('com2',{
		template:'#tmp1',
		data(){
			return{
				msg:'儿子：我有钱了，给爸爸200块钱拿去买烟'
				// sonmsg:{name:'我',agee:21}
			}
		},
		methods:{
			myclick:function(){
				// 当点击子组件，触发拿到父组件传递过来的func方法
				this.$emit('func',123,456,this.msg)
			}
		}
	})

	var vm = new Vue({
		el:'#app',
		data:{
			msg: '爸爸这里有100块钱，儿子你要不要？',
			datamsgForSon: null
		},

		components:{
			// 结论：经过演示发现子组件默认无法访问到父组件data数据
			com1:{
				data(){
				//注意子组件的data数据，并不是通过父组件传递过来的，而是子组件私有的，比如Ajax请求回来的数据，都可以放在data身上
				// data 上的数据都是可读可写的
					return{
						title:'123',
						content:'小名'
					}
				},
				// 注意： 组件种所有props数据都是通过父组件传递给子组件的
				template:'<h1>这是子组件{{parentmsg}}</h1>',
				// props中的数据都是只读的
				props:['parentmsg'] 
				//把父组件传递过来的parentmsg属性，在props定义才能使用这个数据
			}
		},
		methods:{
			// onChange:function(){
			// 	this.parentmsg = "被修改了！"
			// }
			show:function(data,data2,data3){
				console.log('这是调用了子组件show方法'+data+data2+data3)
				// 拿到子组件data数据为父组件data数据赋值
				this.datamsgForSon = data3
			}
		}
	})
```
## 演示地址
[父->子 方法和数据，然后把子组件数据绑定到父data中去](/file/父组件子组件传值.html)

# 组件案例：【评论列表】

```head
	<meta name="viewport" content="width=device-width,initial-scale=1.0,user-scalable=no">
	<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
	<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@3.3.7/dist/css/bootstrap.min.css">
```
```css
		.subtitle{
			width: 300px;
			height: auto;
		}
		.b{
			display: block;
			width: 6px;
			height: auto;
			background: skyblue;
		}
		.subtitle h3{
			width: 300px;
			margin: 0;
			padding:0;
			position: relative;
			left: 18px;
		}
```
```html
		<div id="app">
			<div class="container">				
				<div class="jumbotron">
					<cmt-box @func="loadComments"></cmt-box>
				</div>
				<div class="subtitle">
					<span class="b"><h3>评论区</h3></span>
				</div><hr>
				<div class="media">
					<li v-for="item in list" :key="item.id">
						<div class="media-left media-top">
							<img src="https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=3342714247,4238880061&fm=15&gp=0.jpg"  class="media-object" style="width: 60px">
						</div>
						<div class="media-body">							
									<h4 class="media-heading">评论人：{{item.user}}&nbsp;<span style="font-size: 12px;color: #999">{{item.id | dateFormat}}</span></h4>
									<p>{{item.content}}</p>						
						</div>
					</li>
				</div>
			</div>
		</div>
		<template id="tmp1">
			<div>
				<div class="form-group">
					<label>评论人：</label>
					<input type="text"  v-model="user" class="form-control" v-focus>
				</div>
				<div class="form-group">
					<label>评论内容：</label>
					<textarea class="form-control" v-model="content" @keyup.enter="postComment"></textarea>
				</div>
				<div class="form-group">
					<input type="button" class="btn btn-primary" value="发表评论" @click="postComment">
				</div>
			</div>
		</template>
```
```javascript
		var commentBox ={
			template:'#tmp1',
			data(){
				return{
					user:'',
					content:''
				}
			},
			methods:{
				// 发表评论
				// 分析：发表评论的业务逻辑
				// 1.评论数据放在哪 存localStorage中 localStorage.getItem()
				// 2.先组织一个最新的评论数据对象
				// 3.想办法，把第二步得到评论对象保存到localStorage [只支持存放字符串数据]，调用json.stringify
				// 在保存最新的评论数据之前，要先从localStorage获取到之前的数据{string}，转换成一个数组对象，然后把最新评论Push到整个数组
				// 如果获取到的localStorage中的评论字符串为空或不存在，则可以返回一个'[]',让JSON.parse转换

				// 4.把最新的评论列表数组，再次调用JSON.stringify 转为数组字符串，然后调用 localStorage.setItem()存入文件
				postComment:function(){
					var comment ={id: Date.now(),user: this.user,content: this.content}
					// 从localStorage 中获取所有的评论
					var list = JSON.parse(localStorage.getItem('cmts') || '[]')
					list.unshift(comment)
					console.log(list)
					// 重新保存最新的评论数据
					localStorage.setItem('cmts',JSON.stringify(list))
					this.$emit('func')
					this.user = this.content =''
				}
			}			
		}
		var vm = new Vue({
			el:'#app',
			data:{
				list:[
					{id:Date.now(),user:'李白',content:'大河之水天上来，奔流到海不复回'}
				]
			},
			methods:{
				loadComments:function(){
					// 从本地加载评论列表
					var list = JSON.parse(localStorage.getItem('cmts') || '[]')
					this.list = list
				}
			},
			filters:{
				dateFormat:function(dataStr,pattern){
					// 根据给定的字符串给出特定的时间
					var dt = new Date(dataStr)

					// yyyy-mm-dd
					var y = dt.getFullYear()


					// 月|日|十|分|秒  存在 单 位数，需要用es6字符串组合补位 .padStart(length,value)
					var m = (dt.getMonth()+1).toString().padStart(2,'0')
					var d = (dt.getDate()).toString().padStart(2,'0')
					// return y+'-'+m+'-'+'d'

					if (pattern && pattern.toLowerCase()==='yyyy-mm-dd') {
						return `${y}-${m}-${d}`
					}
					else{
						var hh = (dt.getHours()).toString().padStart(2,'0')
						var mm = (dt.getMinutes()).toString().padStart(2,'0')
						var ss = (dt.getSeconds()).toString().padStart(2,'0')
						return `${y}-${m}-${d} ${hh}:${mm}:${ss}`
					}
				}
			},
			components:{
				'cmt-box':commentBox
			},
			// 实现添加焦点聚集
			directives:{
				'focus':{
					bind:function(el){
						//每当指令绑定到指令上会立即执行这个函数，只执行一次
						// 注意： 在每个函数中，第一个参数永远是el ，表示指令绑定的元素，是一个原生js对象

						// 在元素 刚绑定指令时.还没有插入到DOM中去.这时候调用没作用
						// el.focus()
					},
					inserted:function(el){
						// 表示元素插入到DOM中时候执行这个函数，只执行一次
						el.focus()
					},
					update: function(){
						// 表示元素更新到DOM中时候执行这个函数，可执行多次
					}
				}
			},
			created(){
				this.loadComments()
			}
		})
```
## 演示链接
[演示地址](/file/pl.html)

# 使用ref获取DOM元素和组件引用
```html
		<div id="app">
			<input type="button" name="" value="获取元素" @click="getElement">
			<h1 id="myh3" ref="myh3">我是需要调用的DOM元素</h1>
			<hr>
			<login ref="mylogin"></login>
		</div>
```
```javascript
		var login = {
			template:'<h1>登录组件</h1>',
			data(){
				return{
					msg:'son msg'
				}
			},
			methods:{
				show:function(){
					console.log('调用了子组件的show 方法')
				}
			}
		}
		var vm = new Vue({
			el:'#app',
			data:{
				
			},
			methods:{
				getElement:function(){
					// console.log(document.getElementById('myh3').innerText)
					console.log(this.$refs.myh3.innerText)
					console.log(this.$refs.mylogin.msg)
					this.$refs.mylogin.show()
				}
			},
			components:{
				login
			}
		})
```

## 演示
[ref获取dom+ref获取组件方法，data](/file/refDOM.html)
