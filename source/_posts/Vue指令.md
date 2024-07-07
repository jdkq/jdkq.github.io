---
title: Vue指令
tags:
  - Vue
categories:
  - Vue
  - Vue指令
cover: >-
  https://img1.baidu.com/it/u=3306102985,2313411151&fm=253&fmt=auto&app=138&f=PNG?w=2291&h=500
poster:
  topic: 通过指令能快速解决同步更新问题
  headline: Vue指令
  caption: null
  color: black
abbrlink: 669b9394
date: 2020-04-24 13:12:33
banner:
h1:
---
## v-cloak: 能够解决 插值表达式闪烁的问题（只替代占位符）

```html
<style type="text/css">
	[v-cloak]{
		display: none;
	}
</style>
<div id="app"> 
	<p v-cloak>{{msg}}</p>
	<h4 v-text="msg"></h4>
	<!-- 默认 v-text 是没有闪烁问题的 -->
</div>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script type="text/javascript">
	new Vue({
		el:'#app',
		data:{
			msg: '123'
		}

	})
</script>
```

## v-text 会覆盖元素中原本的内容（不替代占位符）

```html
<div id="app"> 
	<h4 v-text="msg">======</h4>
	<!-- 默认 v-text 是没有闪烁问题的 -->
</div>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script type="text/javascript">
	new Vue({
		el:'#app',
		data:{
			msg: '123'
		}
	})
</script>
```

## v-html 渲染html

```html
<div id="app">
	<div v-html="msg"></div> 	
</div>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script type="text/javascript">
	new Vue({
		el:'#app',
		data:{
			msg: '<h1>哈哈哈！这是一个大大大的h1</h1>'
		}
	})
</script>
```



## V-bind(:) 是在vue中用于绑定`属性`的指令 (单向性，M->V)

```html
<div id="app">
	<!-- v-bind 可以简写为 `:` -->
	<!-- v-bind 中可以写合法的js表达式 -->
	<input type="button" value="按钮"  :title="mytitle">	
</div>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script type="text/javascript">
	new Vue({
		el:'#app',
		data:{
			mytitle: '这是一个自定义的title'
		}
	})
</script>
```

## v-on (@) 用来绑定事件
```html
<div id="app">
	<input type="button" value="按钮" id="btn" @click="show"> 	
</div>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script type="text/javascript">
	new Vue({
		el:'#app',
		data:{
			msg: '<h1>哈哈哈！这是一个大大大的h1</h1>'
		},
		<!-- methods定义了当前vue实例所有可用的方法 -->
		methods:{
			show:function(){
				alert('Hello')
			}
		}
	})
	/*document.getElementById('btn').onclick=function(){
		alert("Hello!")
	}*/
</script>
```

## 案例：跑马灯效果
```html
<!-- 创建一个要控制的区域 -->
<div id="app">
	<input type="button" value="浪起来" @click="lang">
	<input type="button" value="低调" @click="stop">
	<h4>{{ msg }}</h4>
</div>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
<script type="text/javascript">
	// 注意： 在vm实例中，如果想要获取data上的数据，或者 想要调用methods中的 方法，必须通过 this.数据名 来进行访问，这里的this 就表示我么们new出来的 VM 实例对象
	var vm = new Vue({
		el:'#app',
		data:{
			msg: '猥琐发育，别浪~~！',
			intervalID: null //在data上定义一个 定时器id

		},
		methods:{
			lang: function(){
				//console.log(this.msg)
				// ()=> 指向 setInterval() 外部实例
				//this
				if (this.intervalID != null) return;
				this.intervalID = setInterval( ()=> {
					// 获取头字符
					var start = this.msg.substring(0,1)
					// 获取尾字符
					var end = this.msg.substring(1)
					// 重新赋值
					this.msg = end + start
				},400)
				
				// 注意： vm实例会监听自己身上的data 所有属性的改变，一旦改变就会同步到页面中
			},
			stop: function(){
				//停止
				clearInterval(this.intervalID)
				this.intervalID = null
			}
		}
	})
</script>

	//分析
	// 1.给【浪起来】按钮绑定一个点击事件v-on
	// 2.在按钮的事件处理函数中，写业务逻辑代码，拿到msg字符串。做截取操作（substring），把第一个放到最后一个
	// 3.为了实现点击一下自动截取，需要把 2 代码放在定时器


</script>
```
> 演示:

<iframe src="/file/pmd.html" scrolling="false" width="100%" height="100px" frameborder="0"></iframe>

## 事件修饰符

* .stop 阻止冒泡
* .prevent 阻止默认事件
* .capture 添加事件监听器时使用事件捕获
* .self 只当事件在该元素本身（比如不是子元素），触发时回调
* .once 事件只触发一次
* .native 自定义的组件上的绑定原生事件得添加

### .stop 阻止全部冒泡
```html
<style>
	.inner{
		height: 150px;
		background-color: darkcyan;
	}
</style>
<div id="app">
	<div class="inner" @click="divHandler">
		<input type="button" value="戳起来" @click.stop="btnHandler">
	</div>
</div>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
<script type="text/javascript">
	var vm = new Vue({
		el:'#app',
		data:{

		},
		methods:{
			divHandler: function(){
				console.log('这是触发了inner div点击事件')
			},
			btnHandler: function(){
				console.log('按钮点击事件')
			}
		}
	})
</script>
```

![没有.stop时的控制台输出](https://ae01.alicdn.com/kf/H6dddca67ed1c40db8ec96dd84caeacf6w.jpg)
![.stop控制台输出](https://ae01.alicdn.com/kf/H52b7942e0e76478ea5b6e05e7885998ba.jpg)


### .prevent
```html
<div id="app">
	<a href="http://www.baidu.com" @click.prevent="linkClick()">有问题问百度</a>
</div>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
<script type="text/javascript">
	var vm = new Vue({
		el:'#app',
		data:{

		},
		methods:{
			linkClick: function(){
				console.log('触发了链接的点击事件')
			}
		}
	})
</script>
```

### .capture
```html
<style>
	.inner{
		height: 150px;
		background-color: darkcyan;
	}
</style>
<div id="app">
	<!-- 使用 .capture 实现捕获触发事件的机制 -->
	<div class="inner" @click.capture="divHandler">
		<input type="button" value="戳起来" @click="btnHandler">
	</div>
</div>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
<script type="text/javascript">
	var vm = new Vue({
		el:'#app',
		data:{

		},
		methods:{
			divHandler: function(){
				console.log('这是触发了inner div点击事件')
			},
			btnHandler: function(){
				console.log('按钮点击事件')
			}
		}
	})
</script>
```
![.capture 从外到里捕获事件](https://ae01.alicdn.com/kf/H39de5a93f69d4b0bbfe966d156106cc4F.jpg)


### .self 阻止自己冒泡
```html
<style>
	.inner{
		height: 150px;
		background-color: darkcyan;
	}
</style>
<div id="app">
	<!-- 只有点击当前元素才会触发事件处理函数 -->
	<div class="inner" @click.self="divHandler">
		<input type="button" value="戳起来" @click="btnHandler">
	</div>
</div>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
<script type="text/javascript">
	var vm = new Vue({
		el:'#app',
		data:{

		},
		methods:{
			divHandler: function(){
				console.log('这是触发了inner div点击事件')
			},
			btnHandler: function(){
				console.log('按钮点击事件')
			}
		}
	})
</script>
```

### .once
```html
<div id="app">
	<!-- 使用 .once 只触发一次事件函数 --> 
	<a href="http://www.baidu.com" @click.prevent.once="linkClick()">有问题问百度</a>
</div>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
<script type="text/javascript">
	var vm = new Vue({
		el:'#app',
		data:{

		},
		methods:{
			linkClick: function(){
				console.log('触发了链接的点击事件')
			}
		}
	})
</script>
```

## v-model 实现双向数据绑定(双向性数据绑定 表单元素 <-> Model ) `只能运用于表单`
```html
<div id="app">
	<h4>{{ msg }}</h4>

	<input type="text" v-model="msg">
</div>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
<script type="text/javascript">
	var vm = new Vue({
		el:'#app',
		data:{
			msg: '简直完美，没瑕疵'
		},
		methods:{

		}
	})
</script>
```
**案例: 简易计算器**

<iframe src="/file/v-modelCaculator.html" scrolling="false" width="100%" height="100px" frameborder="0"></iframe>

## v-class 绑定样式
```html
<style>
.red{color:red}
.thin{font-weight: 200;}
.italic{font-style:intalic;}
.active{letter-spacing: 0.5em}
</style>

<div id="app">
	<!-- 第一种使用方式直接传送一个数组 class用v-bind绑定 -->
	<h1 :class="['thin','intalic']>这是一个很大很大的H1,大到你无法想象</h1>

	<!-- 在数组使用三值表达式 -->
	<h1 :class="['thin','intalic',flag?'active': '']">这是一个很大很大的H1,大到你无法想象</h1>

	<!-- 通过对象 -->
	<h1 :class="['thin','intalic',{'active': flag}]">这是一个很大很大的H1,大到你无法想象</h1>

	<!-- 在为class 使用v-bind 绑定对象的时候，对象的属性是类名，由于对象的属性可带&不可带引号，所以这里我们就没写引号： 属性的值是一个标识符-->
	<h1 :class="classObj">这是一个很大很大的H1,大到你无法想象</h1>
</div>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
<script type="text/javascript">
	var vm = new Vue({
		el:'#app',
		data:{
			flag: false,
			classObj: {red:true,thin:true,italic:false,active:false}
		},
		methods:{

		}
	})
</script>
```

## .style 内联样式绑定
```html
<div id="app">
	<!-- 对象就是无序键值对的集合 -->
	<!-- 如果属性存在'-'必须加引号 -->
	<h1 :style="[styleObj1,styleObj2]">这是一个h1</h1>
</div>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
<script type="text/javascript">
	var vm = new Vue({
		el:'#app',
		data:{
			styleObj1:{color:'red' ,'font-weight': 200}
			styleObj2:{'font-style','italic'}
		},
		methods:{

		}
	})
</script>
```

## v-for 和 key属性
```html
<div id="app">
	<!-- 遍历数组 -->

	<p v-for="{item,i} in list">索引值：{{i}} ，值： {{item}}</p><hr>

	<!-- v-for循环遍历对象数组 -->
	
	<p v-for="{user,i} in list2">索引值：{{i}} , userid: {{user.id}} , name: {{user.name}}</p><hr>

	<!-- v-for 遍历对象 -->
	<!-- 注意在遍历对象身上的键值对的时候，除了有val、 key ，第三个位置还有个索引 -->

	<p v-for="{val,key,i} in user">值:{{val}},键值：{{key}},索引：{{i}}</p><hr>

	<!-- v-for迭代数字 -->
	<!-- in 后放 普通数组，对象数组，对象，数字 -->
	<!-- 如果使用v-for迭代数字的话，count值从 1 开始 -->

	<p v-for="count in 10">这是第 {{count}} 次循环</p>

</div>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
<script type="text/javascript">
	var vm = new Vue({
		el:'#app',
		data:{
			list:[1,2,3,4,5],
			list2:[
				{id: 1 ,name: 're1'},
				{id: 2 ,name: 're2'},
				{id: 3 ,name: 're3'},
				{id: 4 ,name: 're4'},
			],
			user:{
				id: 1,
				name: '董',
				gender: '男'
			}
		},
		methods:{

		}
	})
</script>
```
**v-for使用注意事项**：

> 2.2.0+ 版本里，当在组件中使用v-for时,key值是`必须的`，`强制数据关联`
> key定义v-for唯一身份
```html
<div id="app">

	<div>
		<label>ID:<input v-model="id"></input></label>
		<label>Name:<input v-model="name"></input></label>
		<input type="button" value="添加" @click="add">
	</div>
	<!-- 注意：v-for 循环的时候，key 属性只能使用number 或取string -->
	<!-- 注意： key在使用的时候必须用v-bind绑定属性指定key值 -->
	<!-- 在组件中使用v-for循环时，或者在特定情况中，如果v-for有问题，必须在使用v-for的同时，指定唯一的字符串/数字，类型：key值 -->
	<p v-for="item in list" :key="item">
		<input type="checkbox">{{item.id}} ----
		{{item.name}}
	</p>
</div>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
<script type="text/javascript">
	var vm = new Vue({
		el:'#app',
		data:{
			id:'',
			name:'',
			list:{
				[id:1,name:'里斯'],
				[id:2,name:'凯'],
				[id:3,name:'二哈'],
				[id:4,name:'小孩']
			}
		},
		methods:{
			add: function(){
				this.list.push({id:this.id,name: this.name})
			}
		}
	})
</script>
```
> 演示:

<iframe src="/file/v-for_key.html" width="100%" frameborder="0"></iframe>

## v-if 每次都会重新删除或创建元素
## v-show 每次不会重新进行DOM的删除和创建操作，只是切换了元素的display:none

```html
<div id="app">
	<input type="button" name="" @click="flag=!flag" value="toggle">

	<!-- v-if 有较高的切换性能消耗 -->
	<h3 v-if="flag">这是一个v-if控制的元素</h3>

	<!-- v-show 有较好的初始渲染消耗 -->
	<h3 v-show="flag">这是使用v-show控制的元素</h3>

</div>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
<script type="text/javascript">
	var vm = new Vue({
		el:'#app',
		data:{
			flag: false
		}
	})
</script>
```
* 如果元素设计到频繁的切换,最好不要用v-if 推荐使用 `v-show`
* 如果元素可能永远也不会显示出来给用户看到,则推荐使用 `v-if`

> 演示:

<iframe src="/file/v-if_orv-show.html" width="100%" frameborder="0"></iframe>


## 过滤器

* 概念：可被用作一些常见文本的格式化

* 用在两个地方： 1.插值表达式  2. v-bind 表达式
 
### 过滤器调用时候的格式 

**定义过滤器**

```
	// 过滤器中的function 第一个参数已经被规定死，永远都是 过滤器 管道符前面传递过来的数据
	Vue.filter('过滤器名称',function(data){
		return data+'123'
	})
```
**源码：**

```html
	<div id="app">
		<p><b>过滤前：</b>{{msg}}</p>
		<p><b>过滤后：</b>{{ msg | msgFormat1 }}</p>
		<p><b>传参过滤后：</b>{{ msg | msgFormat2('疯狂、','帅气无比、','风流倜傥') }}</p>
		<p><b>过滤器可以多次调用：</b>{{ msg | msgFormat1 | test }}</p>
	</div>
	<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
	<script type="text/javascript">

		//定义一个vue全局过滤器
		// msg: 拿到msg数据 arg:传递的数据
		Vue.filter('msgFormat1',function(msg){
			// 正常改变只变一个，所以replace前加正则
			return msg.replace(/单纯/g,'狂妄')
		})

		Vue.filter('msgFormat2',function(msg,arg,arg2,arg3){
			return msg.replace(/单纯/g,arg+arg2+arg3)
		})

		Vue.filter('test',function(msg){
			return msg + '++++++++++++++++++++++++++'
		})

		var vm = new Vue({
			el:'#app',
			data:{
				msg:'曾经，我也是一个单纯的少年，单纯的我，傻傻的问，谁是世界上最单纯的人'
			},
			methods:{}
		})
	</script>
```
**演示：**
<iframe src="/file/demo1.html" width="100%" height="350px" frameborder="0"></iframe>


## 按键修饰符
* .enter
* .tab
* .delete (捕获删除和空格)
* .esc
* .space
* .up
* .down
* .left
* .right
* .键盘码

# 品牌列表案例----

<iframe src="/file/list_vue.html" width="100%" height="400px" frameborder="0"></iframe>