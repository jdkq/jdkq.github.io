---
title: JQuery链式编程
tags:
  - Jquery
categories:
  - Jquery
cover: >-
  https://img1.baidu.com/it/u=3306102985,2313411151&fm=253&fmt=auto&app=138&f=PNG?w=2291&h=500
poster:
  topic: 几个需求小问题
  headline: JQuery链式编程
  caption: null
  color: black
abbrlink: 9c508b41
date: 2020-09-18 11:38:24
banner:
h1:
---


## 需求： 
	
* 页面中有一个按钮,还有一个div
* 点击按钮在div中添加一个p标签内容
* 点击的同时修改div背景颜色


<iframe src="/file/jquery_lianshi.html" scrolling="false" frameborder="0" width="100%" height="210px"></iframe>

```javascript
	$(function() {
		// body...
		// 获取按钮调用点击事件，湖片区div设置p内容，点击按钮设置背景颜色
		$('#btn').click(function(){
			$('#dv').html('<p>这是一个p</p>').css("backgroundColor","red")
		})
		var obj = $('#dv').html('<p>这是一个p</p>')
		document.getElementById('obj').innerHTML = obj
	})	
```
```html
	<input type="button" value="显示效果" id="btn" name="">
	<div id="dv"></div>
	<p>这时候前提是获取的这个div调用对象的返回值必须是：<span id="obj"></span></p>才可以使用链式编程
```

# 案例1

## 需求：

* 获取列表中的每个li,当鼠标进入后，当前li高亮显示
* 点击的时候可以让点击li字体变大
* 字体颜色改变
* 字体改变


<iframe src="/file/jquery_demo1.html" scrolling="false" frameborder="0" width="100%" height="210px"></iframe>

```javascript
	$(function() {
		$('#uu>li').mouseover(function(){
			$(this).css("backgroundColor","red").siblings("li").css("backgroundColor","")
		}).click(function(){
			$(this).css("fontSize","30px").css("color","green").css("fontFamily","宋体")
		})
	})
```
```html
	<ul id="uu">
		<li>第1个</li>
		<li>第2个</li>
		<li>第3个</li>
		<li>第4个</li>
		<li>第5个</li>
	</ul>
```

# 案例2

## 需求：

* 点击按钮，改变value值
* 鼠标进入按钮中，改变按钮宽高
* 鼠标离开按钮背景颜色变成 green


<iframe src="/file/jquery_demo2.html" scrolling="false" frameborder="0" width="100%" height="210px"></iframe>

```javascript
	$(function() {
		$('#btn').click(function(){
			$(this).val('改变了')
		}).mouseover(function(){
			$(this).css({"width":"200px","height":"100px"})
		}).mouseout(function(){
			$(this).css("backgroundColor","green")
		})
	})
```

```html
<input type="button" name="" value="显示效果" id="btn">
```

# 获取兄弟元素的几个方法

1. next() 当前元素之后紧挨着的第一个兄弟元素(👆)
2. nextAll() 当前元素之后所有兄弟元素
3. prev() 当前元素之间的紧邻着的兄弟元素（👇）
4. prevAll() 当前元素之前所有兄弟元素
5. siblings() 当前元素的所有兄弟元素