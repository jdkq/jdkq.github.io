---
title: Vue品牌列表
tags:
  - 前端项目
categories:
  - Web前端
  - Vue项目
cover: >-
  https://img1.baidu.com/it/u=3306102985,2313411151&fm=253&fmt=auto&app=138&f=PNG?w=2291&h=500
poster:
  topic: 利用v-for进行数组遍历并进行增、删、查
  headline: Vue品牌项目
  caption: null
  color: black
abbrlink: ed597b90
date: 2020-05-29 19:10:51
banner:
h1:
---

## 演示
<iframe src="/file/list_vue.html" scrolling="false" frameborder="0" width="100%" height="300px"></iframe>

> 后台接口实在配不了，实际应用中接口都会给定
> 献上源码
```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<title>品牌列表(增删改过滤)</title>
	<meta http-equiv="Content-Security-Policy" content="upgrade-insecure-requests">
	<meta name="viewport" content="width=device-width,initial-scale=1.0,user-scalable=no">
	<link href="https://cdn.bootcss.com/twitter-bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
    <link href="https://cdn.bootcss.com/twitter-bootstrap/3.3.7/css/bootstrap-theme.min.css" rel="stylesheet">
    <script src="http://cdn.bootcss.com/jquery/1.11.1/jquery.min.js"></script>
    <script src="http://cdn.bootcss.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>
	<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
</head>
<body>
	<div id="app">
		<div class="panel panel-primary">
			<div class="panel-heading">
				<h3 class="panel-title">添加品牌</h3>
			</div>
			<div class="panel-body form-inline">

				<label>ID:<input type="text" name="" class="form-control" v-model="id"></label>

				<label>Name:<input type="text" name="" class="form-control" v-model="name" @keyup.enter="add"></label>

				<!-- 在vue中使用事件绑定机制处理函数的时候 加()可以传参 -->

				<input type="button" name="" value="添加" class="btn btn-primary" @click="add">

				<!-- 注意： Vue中所有的指令，在调用的时候都以 v- 开头 -->
				<label v-color="'pink'" v-fontweight="600" v-fontsize="'20'">输入搜索关键字:<input type="text" name="" class="form-control" v-model="keywords" v-focus></label>
			</div>
		</div>
		<table class="table table-bordered table-hover table-striped">
			<thead>
				<tr>
					<th>ID</th>
					<th>名称</th>
					<th>操作时间</th>
					<th>操作</th>
				</tr>
			</thead>
			<tbody>
				<!-- 之前 v-for 中的数据能够直接在data list 中直接渲染过来 -->
				<!-- 现在，定义一个search方法，把关键字传参形式传递search方法 -->
				<!-- 把搜索key返回重新定义list 的data数组 -->
				<tr v-for="item in search(keywords)" :key="item.id">
					<td>{{item.id}}</td>
					<td>{{item.name}}</td>
					<td>{{item.ctime | dateFormat}}</td>
					<td>
						<!-- 阻止默认行为,不刷新 .prevent -->
						<a href="" @click.prevent="del(item.id)">删除</a>
					</td>
				</tr>
			</tbody>
		</table>
	</div>	
	<script type="text/javascript">
		// 全局过滤器
		// pattern 传值 显示具体时间
		// 否则 显示 时间
		// Vue.filter('dateFormat',function(dataStr,pattern){
		// 	// 根据给定的字符串给出特定的时间
		// 	var dt = new Date(dataStr)

		// 	// yyyy-mm-dd
		// 	var y = dt.getFullYear()
		// 	var m = dt.getMonth()+1
		// 	var d = dt.getDate()
		// 	// return y+'-'+m+'-'+'d'

		// 	if (pattern && pattern.toLowerCase()==='yyyy-mm-dd') {
		// 		return `${y}-${m}-${d}`
		// 	}
		// 	else{
		// 		var hh =dt.getHours()
		// 		var mm = dt.getMinutes()
		// 		var ss = dt.getSeconds()
		// 		return `${y}-${m}-${d} ${hh}:${mm}:${ss}`
		// 	}
		// })

		// 2.x 版本自定义全局键盘修饰符
		Vue.config.keyCodes.f2 =113 

		// 使用  Vue.directive() 定义全局指令
		// 其中： 参数1： 指令名称 注意在定义时不需要加 v- 前缀 ，调用时必须加
		// 参数2： 是一个对象，在这个对象身上，有一些指令相关的函数，这些函数可以在待定阶段函数操作
		Vue.directive('focus',{
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

		})
		Vue.directive('color',{
			bind:function(el,binding){
				el.style.color=binding.value
			}
		})

		var vm = new Vue({
			el:'#app',
			data:{
				id: '',
				name: '',
				keywords: '',
				list:[
					{id : 1,name: '奔驰',ctime: new Date()},
					{id : 2,name: '牧马人',ctime: new Date()},
				]
			},
			methods:{
				add: function(){
					//分析
					// 1.获取 id 和 name =>data
					// 2.组织一个对象
					// 3.添加对象到list
					// 4.在vue中已经实现了数据的双向绑定,每当我们修改了data的数据,vue默认监听数据变动,把最新数据应用到页面上
					// 5. 我们更多的是在进行vm 中 model数据的操作,同时在model操作中,指定的业务逻辑操作
					var car = {id : this.id,name: this.name,ctime: new Date()}
					this.list.push(car)
					this.name = this.id = null					
				},
				del: function(id){
					// 根据id删除数据
					// 分析:
					// 1. 如何根据id 找到要删除对象的索引
					// 2. 找到索引直接调用 数组的splice 方法

					// this.list.some((item,i)=>{
					// 	if (item.id == id) {
					// 		//在数组的some方法中,如果return true,就会立刻终止这个数组循环
					// 		this.list.splice(i,1)
					// 		return true
					// 	}
					// })
					// 创建回调
					var index = this.list.findIndex(item=>{
						if (item.id == id) {
							//在数组的some方法中,如果return true,就会立刻终止这个数组循环
							return true
						}
					})
					this.list.splice(index,1)
				},
				search: function(keywords){
					// var newList = []
					// this.list.forEach(item =>{
					// 	if (item.name.indexOf(keywords)!=-1) {
					// 		newList.push(item)
					// 	}
					// })
					// return newList

					//  注意： forEach some filter findIndex  这些都属于数组的新方法
					// 都会对数组每一项进行遍历执行相关的操作

					return this.list.filter(item => {
						// 注意： 在es6中，为字符串提供一个新方法，叫做 String prototype.includes('要包含')
						if (item.name.includes(keywords)){
							return item
						}
					})
				}
			},
			filters:{
				// 创建私有过滤器  条件：名称+处理函数
				// 过滤器调用采取就近原则，若私有跟全局一致，则优先调用私有过滤器
				dateFormat: function(dataStr,pattern){
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
			directives:{ //自定义私有指令
				'fontweight':{
					// 设置字体粗细
					bind: function(el,binding){
						el.style.fontWeight=binding.value
					}
				},
				'fontsize':function(el,binding){
					// 这主意这个函数的你沟通与把代码写到bind跟update中去
					el.style.fontSize=parseInt(binding.value)+'px'
				}
			}
		})
	</script>
</body>
</html>
```

