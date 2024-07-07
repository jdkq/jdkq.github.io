---
title: Markdown指南
tags: Markdown语法
categories:
  - Markdown
cover: >-
  https://img1.baidu.com/it/u=3306102985,2313411151&fm=253&fmt=auto&app=138&f=PNG?w=2291&h=500
poster:
  topic: 文档写法
  headline: Markdown语法
  caption: null
  color: black
abbrlink: e2396fcb
date: 2020-03-12 11:45:00
banner:
h1:
---

<blockquote>
	主要介绍markdown的一些基本语法
	markdown 的语法概述，您可以在github上的任何地方或者你自己的文件中使用markdown 语法（我感觉它类似html的标签）
</blockquote>


<!--more-->

## 标头
{%codeblock%}
# This is an <h1> tag
## This is an <h2> tag
###### This is an <h6> tag
{%endcodeblock%}

## 重点
{%codeblock%}
*This text will be italic*
_This will also be italic_

**This text will be bold**
__This will also be bold__

_You **can** combine them_
{%endcodeblock%}

# 清单

## 无序
{%codeblock%}

* Item 1
* Item 2
  * Item 2a
  * Item 2b

{%endcodeblock%}

## 有序
{%codeblock%}
1. Item 1
1. Item 2
1. Item 3
   1. Item 3a
   1. Item 3b
{%endcodeblock%}

# 图片
{%codeblock%}
![Github Logo](/images/logo.png)
Format: ![alt text](url)
{%endcodeblock%}


# 链接
{%codeblock%}
eg:http://github.com -automatic!
[Github](http://github.com)
{%endcodeblock%}

# 块引用
{%codeblock%}

胖虎说:
>　大熊，你真菜
>　静香是我的了！哈哈哈

{%endcodeblock%}

# 内联代码
{%codeblock%}
｀<addr>｀ 就是用反引号
{%endcodeblock%}