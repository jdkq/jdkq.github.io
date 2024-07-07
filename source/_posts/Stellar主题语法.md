---
title: Stellar主题语法
tags:
  - hexo
categories:
  - hexo
  - Stellar语法
poster:
  topic: 表达类标签
  headline: Stellar主题语法
  caption: null
  color: black
cover: >-
  https://img1.baidu.com/it/u=3306102985,2313411151&fm=253&fmt=auto&app=138&f=PNG?w=2291&h=500
abbrlink: 1fd92ba7
date: 2023-10-28 23:56:30
description:
banner:
h1:
---

{% timeline api:https://api.github.com/repos/xaoxuu/hexo-theme-stellar/releases?per_page=1 %}
{% endtimeline %}

## emoji标签 
{% tabs active:2 align:center %}

<!-- tab 源码 -->
```yaml
{% emoji 爱你 %}
{% emoji blobcat ablobcatrainbow %}
{% emoji blobcat ablobcatattentionreverse %}
{% emoji tieba 滑稽 %}
```

<!-- tab 效果展示 -->
{% emoji 爱你 %}
{% emoji blobcat ablobcatrainbow %}
{% emoji blobcat ablobcatattentionreverse %}
{% emoji tieba 滑稽 %}

{% endtabs %}


配置文件文件名用`${name}`代替
```yaml
tag_plugins:
  emoji:
    default: https://gcore.jsdelivr.net/gh/cdn-x/emoji/qq/${name}.gif
    twemoji: https://gcore.jsdelivr.net/gh/twitter/twemoji/assets/svg/${name}.svg
    qq: https://gcore.jsdelivr.net/gh/cdn-x/emoji/qq/${name}.gif
    aru: https://gcore.jsdelivr.net/gh/cdn-x/emoji/aru-l/${name}.gif
    tieba: https://gcore.jsdelivr.net/gh/cdn-x/emoji/tieba/${name}.png
```

## mark 行内文本标记
{% tabs active:2 align:center %}
<!-- tab 演示效果 -->
支持多彩标记，包括：{% mark 默认 %} {% mark 红 color:red %} {% mark 橙 color:orange %} {% mark 黄 color:yellow %} {% mark 绿 color:green %} {% mark 青 color:cyan %} {% mark 蓝 color:blue %} {% mark 紫 color:purple %} {% mark 浅 color:light %} {% mark 深 color:dark %} {% mark 警告 color:warning %} {% mark 错误 color:error %} 一共 12 种颜色。

<!-- tab 源码 -->
```yaml
支持多彩标记,包括：{% mark 默认 %}{% mark 红 color:red %} {% mark 橙 color:orange %} {% mark 黄 color:yellow %} {% mark 绿 color:green %} {% mark 青 color:cyan %} {% mark 蓝 color:blue %} {% mark 紫 color:purple %} {% mark 浅 color:light %} {% mark 深 color:dark %} {% mark 警告 color:warning %} {% mark 错误 color:error %} 一共 12 种颜色。
```
{% endtabs %}



可供选择文本标记color：red、orange、yellow、green、cyan、blue、purple、light、dark、warning、error
格式：`{% mark 文本 color:xxx %}`

## tag 标签
这个效果类似于 mark 标签，但是更适合一批标签独占一行来使用，支持链接
{% tag 西瓜视频 https://www.ixigua.com/ %}
{% tag 瑞星咖啡官网 https://www.lkcoffee.com/ color:blue %}
如果没有指定颜色，且没有设置默认颜色，则随机取一个颜色

```yaml
{% tag 西瓜视频 https://www.ixigua.com/ %}
{% tag 瑞星咖啡官网 https://www.lkcoffee.com/ color:blue %}
```

## image 图片标签
图片标签是一个精心设计的应对各种尺寸插图的标签，对于大图，可以放置一个「下载」按钮，语法格式如下：
```yaml
{% image src [description] [download:bool/string] [width:px] [padding:px] [bg:hex] %}
```
{% mark src: color:light %} 地址 </br>
{% mark description: color:light %} 图片描述 </br>
{% mark download: color:light %} 下载地址 </br>
{% mark width: color:light %}  图片宽度 </br>
{% mark padding: color:light %} 16px 图片四周填充宽度 </br>
{% mark bg: color:light %} 图片区域背景色 </br>

## 大尺寸图片

无论在什么宽度的设备上都希望横向铺满的图片，一般不需要额外操作。可以在链接后面写上图片描述，如有必要，可以通过设置 `download:true `使其显示一个「下载」按钮链接指向图片地址，如果下载链接与显示的图片地址不同，可以 `download:下载链接`来使其能够下载原图。

{% image https://xaoxuu.com/assets/wiki/stellar/photos/183e71e0ad995.jpg 来自印度的 Rohit Vohra 使用 iPhone 12 Pro Max 拍摄。 download:true %}
{% image https://xaoxuu.com/assets/wiki/stellar/photos/bc7bda18328da.jpg 来自澳大利亚的 Pieter de Vries 使用 iPhone 12 Pro Max 拍摄。 download:https://xaoxuu.com/assets/wiki/stellar/photos/bc7bda18328da.jpg %}

```yaml
{% image https://xaoxuu.com/assets/wiki/stellar/photos/183e71e0ad995.jpg 来自印度的 Rohit Vohra 使用 iPhone 12 Pro Max 拍摄。 download:true %}
{% image https://xaoxuu.com/assets/wiki/stellar/photos/bc7bda18328da.jpg 来自澳大利亚的 Pieter de Vries 使用 iPhone 12 Pro Max 拍摄。 download:https://xaoxuu.com/assets/wiki/stellar/photos/bc7bda18328da.jpg %}
```

## 小尺寸图片优化

### 有底色图片
{% image https://img0.baidu.com/it/u=31487413,442391827&fm=253&fmt=auto&app=138&f=JPEG?w=889&h=500  width:600px padding:16px bg:white %}

```yaml
{% image https://img0.baidu.com/it/u=31487413,442391827&fm=253&fmt=auto&app=138&f=JPEG?w=889&h=500  width:200px padding:16px bg:white %}
```

### 无底色图片
没有底色的图片，可以填充 `bg:var(--card)`动态颜色，能够适配暗黑模式
{% image https://img2.baidu.com/it/u=925686306,4047937547&fm=253&fmt=auto&app=138&f=JPEG?w=825&h=500 bg:var(--card) padding:16px %}

```yaml
{% image  https://img2.baidu.com/it/u=925686306,4047937547&fm=253&fmt=auto&app=138&f=JPEG?w=825&h=500 width:200px padding:16px bg:white %}
```

## quot 引用
适合居中且醒目的引用：
{% quot 我是这世界最帅的男人 %}

支持自定义的引号：
{% quot 热门话题 icon:hashtag %}

特别引用：可以当标题用
{% quot 热门话题 el:h3 %}

```yaml
适合居中且醒目的引用：
{% quot Stellar 是最好用的主题 %}
支持自定义引号：
{% quot 热门话题 icon:hashtag %}
特别引用：可以当标题用
{% quot 热门话题 el:h3 %}
```

## note 备注块
```yaml
{% note [title] content [color:color] %}
# title: 标题（可选）
# content: 内容
# color: red/orange/yellow/green/cyan/blue/purple/light/dark/warning/error
```
{% note 一共支持12种颜色，可以满足几乎所有的需求了。 color 可设置 red、orange、yellow、green、cyan、blue、purple、light、dark、warning、error 几种取值。 %}
{% note 一共支持12种颜色，可以满足几乎所有的需求了。 color 可设置 red、orange、yellow、green、cyan、blue、purple、light、dark、warning、error 几种取值。 color:red %}
{% note 一共支持12种颜色，可以满足几乎所有的需求了。 color 可设置 red、orange、yellow、green、cyan、blue、purple、light、dark、warning、error 几种取值。 color:orange %}
{% note 一共支持12种颜色，可以满足几乎所有的需求了。 color 可设置 red、orange、yellow、green、cyan、blue、purple、light、dark、warning、error 几种取值。 color:yellow %}
{% note 一共支持12种颜色，可以满足几乎所有的需求了。 color 可设置 red、orange、yellow、green、cyan、blue、purple、light、dark、warning、error 几种取值。 color:green %}
{% note 一共支持12种颜色，可以满足几乎所有的需求了。 color 可设置 red、orange、yellow、green、cyan、blue、purple、light、dark、warning、error 几种取值。 color:cyan %}
{% note 一共支持12种颜色，可以满足几乎所有的需求了。 color 可设置 red、orange、yellow、green、cyan、blue、purple、light、dark、warning、error 几种取值。 color:blue %}
{% note 一共支持12种颜色，可以满足几乎所有的需求了。 color 可设置 red、orange、yellow、green、cyan、blue、purple、light、dark、warning、error 几种取值。 color:purple %}
{% note 一共支持12种颜色，可以满足几乎所有的需求了。 color 可设置 red、orange、yellow、green、cyan、blue、purple、light、dark、warning、error 几种取值。 color:light %}
{% note 一共支持12种颜色，可以满足几乎所有的需求了。 color 可设置 red、orange、yellow、green、cyan、blue、purple、light、dark、warning、error 几种取值。 color:dark %}
{% note 一共支持12种颜色，可以满足几乎所有的需求了。 color 可设置 red、orange、yellow、green、cyan、blue、purple、light、dark、warning、error 几种取值。 color:warning %}
{% note 一共支持12种颜色，可以满足几乎所有的需求了。 color 可设置 red、orange、yellow、green、cyan、blue、purple、light、dark、warning、error 几种取值。 color:error %}

## link 链接卡片

不带摘要的样式：
{% link https://xaoxuu.com/blog/20221029/ %}
带摘要的样式：
{% link https://xaoxuu.com/blog/20221029/ desc:true %}

```yaml
{% link href [title] [icon:src] [desc:true/false] %}
# href: 链接
# title: 可选，手动设置标题（为空时会自动抓取页面标题）
# icon: 可选，手动设置图标（为空时会自动抓取页面图标）
# desc: 可选，是否显示摘要描述，为true时将会显示页面描述
```

## radio 单选

{% radio 没有勾选的单选框 %}
{% radio checked:true 已勾选的单选框 %}
```yaml
{% radio 没有勾选的单选框 %}
{% radio checked:true 已勾选的单选框 %}
# checked: true/false
# color: red/orange/yellow/green/cyan/blue/purple
```

## checkbox 复选
{% checkbox 普通的没有勾选的复选框 %}
{% checkbox checked:true 普通的已勾选的复选框 %}
{% checkbox symbol:plus color:green checked:true 显示为加号的绿色的已勾选的复选框 %}
{% checkbox symbol:minus color:yellow checked:true 显示为减号的黄色的已勾选的复选框 %}
{% checkbox symbol:times color:red checked:true 显示为乘号的红色的已勾选的复选框 %}
```yaml
{% checkbox 普通的没有勾选的复选框 %}
{% checkbox checked:true 普通的已勾选的复选框 %}
{% checkbox symbol:plus color:green checked:true 显示为加号的绿色的已勾选的复选框 %}
{% checkbox symbol:minus color:yellow checked:true 显示为减号的黄色的已勾选的复选框 %}
{% checkbox symbol:times color:red checked:true 显示为乘号的红色的已勾选的复选框 %}
# checked: true/false
# color: red/orange/yellow/green/cyan/blue/purple
# symbol: plus/minus/times
```

## navbar 导航栏
{% navbar active:1 [文章](/) [标签](/tags/)  [GitHub](https://github.com/jdkq/) %}

```yaml
{% navbar active:1 [文章](/) [标签](/tags/)  [GitHub](https://github.com/jdkq/) %}
```


## frame 设备框架
{% frame iphone11 img:https://img2.baidu.com/it/u=638285213,1746517464&fm=253&fmt=auto&app=120&f=JPEG?w=1422&h=800 video:/assets/wiki/prohud/toast/demo-loading.mp4  focus:top %}

```yaml
{% frame iphone11 img:/assets/wiki/prohud/toast/demo-loading.png video:/assets/wiki/prohud/toast/demo-loading.mp4 focus:top %}
```
## 文本修饰标签集
- 这是 {% psw 密码 %} 标签
- 这是 {% u 下划线 %} 标签
- 这是 {% emp 着重号 %} 标签
- 这是 {% wavy 波浪线 %} 标签
- 这是 {% del 删除线 %} 标签
- 这是 {% sup 上角标 color:red %} 标签
- 这是 {% sub 下角标 %} 标签
- 这是 {% kbd 键盘样式 %} 标签，试一试：{% kbd ⌘ %} + {% kbd D %}
```yaml
- 这是 {% psw 密码 %} 标签
- 这是 {% u 下划线 %} 标签
- 这是 {% emp 着重号 %} 标签
- 这是 {% wavy 波浪线 %} 标签
- 这是 {% del 删除线 %} 标签
- 这是 {% sup 上角标 color:red %} 标签
- 这是 {% sub 下角标 %} 标签
- 这是 {% kbd 键盘样式 %} 标签，试一试：{% kbd ⌘ %} + {% kbd D %}
```

## 时间线
{% timeline %}
<!-- node 2021 年 2 月 16 日 -->
主要部分功能已经开发的差不多了。
{% image https://img1.baidu.com/it/u=676729016,138144393&fm=253&fmt=auto&app=138&f=PNG?w=889&h=500 width:300px %}
<!-- node 2021 年 2 月 11 日 -->
今天除夕，也是生日，一个人在外地过年+过生日，熬夜开发新主题，尽量在假期结束前放出公测版。
{% endtimeline %}

```yaml
{% timeline %}
<!-- node 2021 年 2 月 16 日 -->
主要部分功能已经开发的差不多了。
{% image https://img1.baidu.com/it/u=676729016,138144393&fm=253&fmt=auto&app=138&f=PNG?w=889&h=500 width:300px %}
<!-- node 2021 年 2 月 11 日 -->
今天除夕，也是生日，一个人在外地过年+过生日，熬夜开发新主题，尽量在假期结束前放出公测版。
{% endtimeline %}
```

## ghcard 卡片
{% ghcard Marcus %}
{% ghcard jdkq/Web theme:dark %}
```yaml
{% ghcard Marcus %}
{% ghcard jdkq/Web theme:dark %}
```

## ablock 普通块容器
note 标签就是使用 ablock 容器实现的，它们样式是相同的：
{% ablock Stellar v1.12.0 color:warning %}
因为原 noteblock 标签在升级到 hexo 6.0 之后跟官方库冲突了，官方一直没有解释原因，后不得不改名：
noteblock -> grid -> border
详情见：[#172](https://github.com/volantis-x/hexo-theme-volantis/issues/712)
{% endablock %}
```yaml
# {% ablock [title] [color:color] [child:codeblock/tabs] %}
# ...
# {% endablock %}

{% ablock Stellar v1.12.0 color:warning %}
因为原 noteblock 标签在升级到 hexo 6.0 之后跟官方库冲突了，官方一直没有解释原因，后不得不改名：
noteblock -> grid -> border
详情见：[#172](https://github.com/volantis-x/hexo-theme-volantis/issues/712)
{% endablock %}
```

## folding 折叠容器


{% folding 这里有个猪头   open:false color:light %}
你居然信了！{% emoji blobcat ablobcatattentionreverse %}
{% endfolding %}

```
{% folding 这里有个猪头  open:false color:light %}
你居然信了！{% emoji blobcat ablobcatattentionreverse %}
{% endfolding %}
```

## tabs 分栏容器 (拆NEXT的效果)
{% tabs active:2 align:center %}

<!-- tab 图片 -->
{% image https://img1.baidu.com/it/u=676729016,138144393&fm=253&fmt=auto&app=138&f=PNG?w=889&h=500 width:300px %}

<!-- tab 代码块 -->
```swift
let x = 123
print("hello world")
```

<!-- tab 表格 -->
| a | b | c |
| --- | --- | --- |
| a1 | b1 | c1 |
| a2 | b2 | c2 |

{% endtabs %}

```
{% tabs active:2 align:center %}

<!-- tab 图片 -->
{% image https://img1.baidu.com/it/u=676729016,138144393&fm=253&fmt=auto&app=138&f=PNG?w=889&h=500 width:300px %}

<!-- tab 代码块 -->
```swift
let x = 123
print("hello world")


<!-- tab 表格 -->
| a | b | c |
| --- | --- | --- |
| a1 | b1 | c1 |
| a2 | b2 | c2 |

{% endtabs %}
```




### swiper 轮播容器

{% swiper effect:cards %}
![](https://images.unsplash.com/photo-1625171515821-1870deb2743b?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=774&q=80)
![](https://images.unsplash.com/photo-1528283648649-33347faa5d9e?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=774&q=80)
![](https://images.unsplash.com/photo-1542272201-b1ca555f8505?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=774&q=80)
![](https://images.unsplash.com/photo-1524797905120-92940d3a18d6?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=774&q=80)
{% endswiper %}

```yaml
{% swiper effect:cards %}
![](https://images.unsplash.com/photo-1625171515821-1870deb2743b?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=774&q=80)
![](https://images.unsplash.com/photo-1528283648649-33347faa5d9e?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=774&q=80)
![](https://images.unsplash.com/photo-1542272201-b1ca555f8505?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=774&q=80)
![](https://images.unsplash.com/photo-1524797905120-92940d3a18d6?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=774&q=80)
{% endswiper %}
```