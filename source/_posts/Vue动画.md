---
title: vue动画
tags:
  - Vue
categories:
  - Vue
  - Vue动画
cover: >-
  https://img1.baidu.com/it/u=3306102985,2313411151&fm=253&fmt=auto&app=138&f=PNG?w=2291&h=500
poster:
  topic: 使用过度动画提高渲染效果
  headline: Vue动画
  caption: null
  color: black
abbrlink: 88bda290
date: 2020-05-31 15:13:20
banner:
h1:
---
![进入/离开的过渡](https://cn.vuejs.org/images/transition.png)

# 共用 v-
```cs
	/*自定义两组样式控制transition 内部元素实现过渡动画 */
	/* v-enter 进入前，元素起始状态 [时间点]*/
	.v-enter,
	/* v-leave-to 离开之后时间点*/
	.v-leave-to{
		opacity: 0;
		transform: translate(200px);
	}
	/* v-enter-active [入场动画时间段]*/
	/* v-leave-active [离场动画时间段]*/
	.v-enter-active,
	.v-leave-active{
		transition: all 0.4s ease;
	}
```
```html
	<div id="app">
		<p>需求: 使用过度类名实现动画点击h3显示，再点击隐藏</p>
		<input type="button" name="" value="toggle" @click="flag=!flag">
		<!-- 使用transtion 元素把需要的被动画控制的元素 -->
		<transition>
			<h3 v-if="flag">这是一个h3</h3>
		</transition>
		<hr>
		<input type="button" name="" value="toggle2" @click="flag2=!flag2">
		<!-- 使用transtion 元素把需要的被动画控制的元素 -->
		<transition>
			<h6 v-if="flag2">这是一个h6</h6>
		</transition>		
	</div>
```
```javascript
		var vm = new Vue({
			el:'#app',
			data:{
				flag: false,
				flag2: false
			},
			methods:{},
		})
```
## 演示
<iframe src="/file/vue动画.html" scrolling="false" width="100%" height="300px" frameborder="0"></iframe>


# 自定义v-前缀

> 注意：添加两组transition类区别有无name属性
```cs
	/* v-enter 进入前，元素起始状态 [时间点]*/
	.v-enter,
	/* v-leave-to 离开之后时间点*/
	.v-leave-to{
		opacity: 0;
		transform: translateX(200px);
	}
	/* v-enter-active [入场动画时间段]*/
	/* v-leave-active [离场动画时间段]*/
	.v-enter-active,
	.v-leave-active{
		transition: all 0.4s ease;
	}

	/* v-enter 进入前，元素起始状态 [时间点]*/
	.my-enter,
	/* v-leave-to 离开之后时间点*/
	.my-leave-to{
		opacity: 0;
		transform: translateY(200px);
	}
	/* v-enter-active [入场动画时间段]*/
	/* v-leave-active [离场动画时间段]*/
	.my-enter-active,
	.my-leave-active{
		transition: all 0.4s ease;
	}
```
```html
	<div id="app">
		<p>需求: 使用过度类名实现动画实现 上面按钮从右向左 下面从下到上</p>
		<input type="button" name="" value="toggle" @click="flag=!flag">
		<!-- 使用transtion 元素把需要的被动画控制的元素 -->
		<transition>
			<h3 v-if="flag">这是一个h3</h3>
		</transition>
		<hr>
		<input type="button" name="" value="toggle2" @click="flag2=!flag2">
		<!-- 使用transtion 元素把需要的被动画控制的元素 -->
		<!-- 注意：name="my" -->
		<transition name="my">  
			<h6 v-if="flag2">这是一个h6</h6>
		</transition>
		
	</div>
```
```javascript
		var vm = new Vue({
			el:'#app',
			data:{
				flag: false,
				flag2: false
			},
			methods:{},
		})
```
## 演示

<iframe src="/file/自定义v-前缀.html" scrolling="false" width="100%" height="300px" frameborder="0"></iframe>

# 第三方动态库实现动画
> 如：https://animate.style/

## 源码
```html
	<link href="https://cdn.jsdelivr.net/npm/animate.css@3.5.1" rel="stylesheet" type="text/css">
```
```html
	<div id="app">
		<div id="example-3">
		  <button @click="flag = !flag">
		    toggle
		  </button>
		  <transition
		    name="custom-classes-transition"
		    enter-active-class="animated tada"
		    leave-active-class="animated bounceOutRight"
		  >
		    <p v-if="flag">Animate.css</p>
		  </transition>
		</div>
	</div>
```
```javascript
		var vm = new Vue({
			el:'#example-3',
			data:{
				flag: false
			},
			methods:{},
		})
```

## 演示
<iframe src="/file/animate.html"  width="100%" height="300px" frameborder="0"></iframe>


# 半场动画（例如加入购物车）【借助于  函数】
```html
	<transition
	  v-on:before-enter="beforeEnter"
	  v-on:enter="enter"
	  v-on:after-enter="afterEnter"
	  v-on:enter-cancelled="enterCancelled"

	  v-on:before-leave="beforeLeave"
	  v-on:leave="leave"
	  v-on:after-leave="afterLeave"
	  v-on:leave-cancelled="leaveCancelled"
	>
	  <!-- ... -->
	</transition>
```

## 演示
[钩子小球动画](/file/钩子小球动画.html)


## 代码
```cs
	body{
		color: #fff;
		background-color: #000
	}
	.ball{
		width: 15px;
		height: 15px;
		background-color: red;
		border-radius: 50%
	}
	input[type="button"]:hover{
		cursor: pointer;
	}
```
```html
	<div id="app">
		<input type="button" value="快到碗里来" name="" @click="flag=!flag">
		<!-- 使用transtion包裹元素 -->
		<transition
			@before-enter="beforeEnter"
			@enter="enter"
			@after-enter="afterEnter">
			<div class="ball" v-show="flag"></div>
		</transition>
		<span style="position: absolute;left: 120px;top: 500px">“形象”的碗</span>
		
	</div>
```
```javascript
		var vm = new Vue({
			el:'#app',
			data:{
				flag: false
			},
			methods:{
				// el:表示要执行动画的那个元素是个原生的js DOM对象
				// el是通过 document.getElmentById('') 获取的DOM对象
				beforeEnter:function (el) {
					// 表示动画入场之前，此时动画尚未开始，可以在beforeEnter 中设置动画开始之前的其实样式
					// 设置小球起始位置
					el.style.transform = "translate(0,0)"
				},
				enter: function (el,done){
					// 这句话没有实际作用，如果不写没有实际效果
					// 可以el.offsetWidth会强制浏览器刷新
					el.offsetWidth
					// 表示动画开始之后的样式，这里可以设置小球完成动画的结束状态
					el.style.transform = "translate(150px,450px)"
					el.style.transition = "all 1s ease"

					// 这里的回调done函数 ，其实就是 afterEnter 这个函数，也就是说done是afterEnter的引用
					done()
				},
				afterEnter: function (el){
					// 动画完成之后
					// 这句话 ：第一个功能：控制小球的显示与隐藏
					// 第二个功能： 直接跳过后半场动画，让flag 变成false
					// 当第二次点击， flag:false -> true
					this.flag = !this.flag
					
					// el.style.opacity=0

					// Vue 把一个完整的动画使用钩子函数拆分成了两部分
					// 我们使用 flag 标识符表示动画的切换

					// flag = flase -> true ->false
				}
			},
		})
```


# transition-group 列表动画

## 源码
```cs
	ul{
		padding: 0
	}
	li{
		width: 100%;
		list-style-type: none;
		border: 1px dashed #999;
		padding: 8px;
		line-height: 35px;

	}
	li:hover{
		background-color: pink;
		transition: all 0.4s ease
	}
	.v-enter,
	.v-leave-to{
		opacity: 0;
		transform: translateY(80px);
	}
	.v-enter-active,
	.v-leave-active{
		transition: all 0.8s ease
	}
	/*
		下面的.move 和 .v-leave-active 配合使用，能够实现列表后续的元素，渐渐的飘上来的效果
	*/
	.v-move{
		transition: all 0.8s ease
	}
	.v-leave-active{
		position: absolute;
	}
```
```html
	<div id="app">
		<div>
			<label>
				ID:
				<input type="text" name="" v-model="id">
			</label>
			<label>
				Name:
				<input type="text" name="" v-model="name">
			</label>
			<input type="button" name="" value="添加" @click="add">
		</div>
			<!-- 在实现列表过度的时候，如果需要过度元素，是通过v-for 循环渲染出来的，需要用transition包裹 所以使用transitionGroup -->
			<!-- 如果要给 v-for 循环创建元素动画，必须为每一个元素设置:key -->
			<p>奸臣一表：【点击删除】</p>
			<transition-group appear tag="ul">
				<li v-for="item in list" :key="item.id" @click="del(item.id)">
					{{item.id}} ---- {{item.name}}
				</li>
			</transition-group>
			
	</div>
```
```javascript
		var vm = new Vue({
			el:'#app',
			data:{
				id: '',
				name: '',
				list:[
					{id:1,name:'赵高'},
					{id:2,name:'魏忠贤'},
					{id:3,name:'脑补不出来'},
					{id:4,name:'你们来吧'}
				]
			},
			methods:{
				add: function(){
					this.list.push({id:this.id,name:this.name})
					this.id = this.name =''
				},
				del:function(id){
					var index = this.list.findIndex(item=>{
						if (item.id == id) {
							//在数组的some方法中,如果return true,就会立刻终止这个数组循环
							return true
						}
					})
					this.list.splice(index,1)
					}
			},
		})
```
## 演示
<iframe src="/file/list动画.html"  width="100%" height="400px" frameborder="0"></iframe>


**注意：我们发现 `transition-group` 渲染成一个span标签，span标签内包含v-for 遍历的list数组，不符合`w3c`的行内元素不能包裹块状元素的原则，所以需要给`transition-group` 加一个tag属性渲染`ul`,若不指定默认渲染为`span`。**