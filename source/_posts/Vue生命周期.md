---
title: Vue生命周期
tags:
  - Vue
categories:
  - Vue
  - Vue生命周期
cover: >-
  https://img1.baidu.com/it/u=3306102985,2313411151&fm=253&fmt=auto&app=138&f=PNG?w=2291&h=500
poster:
  topic: 创建、初始化、为渲染、渲染、销毁更新5个步骤的函数方法
  headline: Vue生命周期
  caption: null
  color: black
abbrlink: 83f13096
date: 2020-05-27 15:31:24
banner:
h1:
---
# Vue实例的生命周期

概念：从Vue实例的创建、运行、到销毁期间，总是伴随着各种各样的时间，这类事件统称为生命周期

`生命周期钩子 = 生命周期函数 = 生命周期事件`

生命周期函数分：
* 创建
* 运行
* 销毁

![vue实例生命周期图例](https://cn.vuejs.org/images/lifecycle.png)

## 创建

```html
	<div id="app">
		<h3 id="h">{{ msg }}</h3>
	</div>
	<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
	<script type="text/javascript">
		var vm = new Vue({
			el:'#app',
			data:{
				msg: 'ok'
			},
			methods:{
				show: function(){
					console.log('show调用')
				}
			},
			beforeCreate(){
				//这里时我们遇到的第1个生命周期函数，表示实例完全被创建出来之前，会执行它
				// this.show()
				// 注意：  在 beforeCreate() 生命周期函数执行的时候，data,methods 都没有初始化
			},
			created(){
				// 这是遇到的第2个生命周期函数
				this.show()
				// 在 created 中，data和methods都已经被初始画
				// 如果我们需要调用methods方法就只能在这里写
			},
			beforeMount(){
				// 这是遇到的第3个生命周期函数，表示模板已经在内存中编辑完成,但尚未把模板渲染到页面
				console.log(document.getElementById('h').innerText)

				// 在beforeMount执行的时候，页面元素还没有真正替换过来，只是模板字符串
			},
			mounted(){
				//这是遇到的第4个生命周期函数，表示内存中的模板已经真是的挂载到页面，用户可以看到渲染的页面了
				console.log(document.getElementById('h').innerText)
				// 注意： mounted 是实例创建期间最后一个生命周期函数，当执行完mounted 就表示实例已被完全创建，此时如果没有其他操作的话，这个实例就静静的躺在我们的内存中一动不动
			}
		})
	</script>
```

> 如果要通过某些插件操作页面上的DOM节点，最早要在 `mounted` 中执行
> 只要执行完 `mounted` ，就表示整个Vue实例已经初始化完毕了。此时，组件已经脱离了创建阶段，进入到运行阶段


## 运行

```html
	<div id="app">
		<h3 id="h">{{ msg }}</h3>
		<input type="button" name="" value="修改msg" @click="msg='no'">
	</div>
	<script type="text/javascript">
		var vm = new Vue({
			el:'#app',
			data:{
				msg: 'ok'
			},
			methods:{
				show: function(){
					console.log('show调用')
				}
			}
			// 接下来是运行中的两个事件
			beforeUpdate(){
				// 这时候表示数据肯定被更新了
				console.log('界面上元素的内容'+document.getElementById('h').innerText)
				console.log('data中的msg:'+this.msg)

				// 当执行时，页面内容还是旧的，data是最新的
			},
			updated(){
				console.log('界面上元素的内容'+document.getElementById('h').innerText)
				console.log('data中的msg:'+this.msg)
				// updated执行完 数据和页面元素都是最新的
			}
		})
	</script>
```

## 销毁

* beforeDestory()：当执行此函数时，Vue实例已经从运行阶段进入销毁阶段
可执行此函数时，实例身上所有`data`、`methods` 以及 `过滤器`、`指令`等等都处于可用状态，此时还没有真正执行销毁的过程。

* destroyed(): 当执行此函数时，组件已被完全销毁，此时，组件中所有数据、方法、指令、过滤器都销毁了


### 演示：
[点击这里查看页面](/file/vue_sdate.html)