---
title: MVC跟MVVM
tags:
  - MVC和MVVM
categories:
  - Web前端
  - MVC和MVVM
  - Vue
cover: >-
  https://img1.baidu.com/it/u=3306102985,2313411151&fm=253&fmt=auto&app=138&f=PNG?w=2291&h=500
poster:
  topic: Node (后端) 中的MVC与前端中的MVVM之间的区别跟概念
  headline: MVC跟MVVM
  caption: null
  color: black
abbrlink: af8177f5
date: 2020-04-24 12:21:18
banner:
sticky: 100
h1:
---

## Node后端中的MVC与前端中的MVVM之间的区别跟概念

{% tabs active:1 align:center %}
<!-- tab MVC -->
{% image https://imgconvert.csdnimg.cn/aHR0cHM6Ly9wLnBzdGF0cC5jb20vb3JpZ2luL2ZlNmUwMDAxMWFmYzUxNTQ5NWNi?x-oss-process=image/format,png  mvc构成图示 download:true %}

<!-- tab MVVM -->
{% image https://imgconvert.csdnimg.cn/aHR0cHM6Ly9wLnBzdGF0cC5jb20vb3JpZ2luL2ZlMmQwMDAxMWE2MTRiNWE2NDMz?x-oss-process=image/format,png  mvvm构成图示 download:true %}

{% endtabs %}

## 对应关系
{% note MVC M: model处理数据的crud</br>V: view</br>C:业务逻辑处理层 登录&&注销  color:dark %}
{% note MVVM  M: model处理数据的crud</br>V: view</br>Vm: 是M跟V的调度者   color:green %}

## 拿ES6支持下的Vue代码来举例
{% tabs active:1 align:center %}
<!-- tab Vue的代码 -->
```html
<div id="app">
	<p>{{ msg }}</p>
</div>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
	// 创建vue实例
	//当我们导入包之后，在浏览器内存中，就多了个vue构造函数
	var vm = new Vue({
		el: '#app', //vue实例控制页面哪个区域
		data:{
			//存放的是el中的数据
			msg: '存放学习VUE' //通过vue提供的指令很方便的渲染到页面上，程序员不再手动操作dom元素了[前端的vue之类的框架。不提倡我们手动去操作dom]
		}	
	})
</script>
```
<!-- tab 代码对应mvvm截图 -->
{% image https://imgconvert.csdnimg.cn/aHR0cHM6Ly9wLnBzdGF0cC5jb20vb3JpZ2luL2ZlZjgwMDAwOGZkMDNkNWMxNGEx?x-oss-process=image/format,png vue mvvm结构 download:true %}
{% endtabs %}