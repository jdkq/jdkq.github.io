---
title: Vue小项目Excel解析为Word
tags:
  - 前端项目
categories:
  - Web前端
  - Vue项目
cover: >-
  https://img1.baidu.com/it/u=3306102985,2313411151&fm=253&fmt=auto&app=138&f=PNG?w=2291&h=500
poster:
  topic: 利用v-for进行数组遍历并查询导出【html/word文件形式】
  headline: Vue小项目Excel解析为Word
  caption: null
  color: black
abbrlink: a0114c0d
date: 2020-06-22 10:44:58
banner:
h1:
---
# 分析

前段时间有一朋友说有个需求，所以我就利用自己所学的vue做一个实战练习

> 需求：`excel考试题目`转换成`word`

> 需要的依赖 : xlsx的一个包

*因为涉及转换而且利用官方推荐的`迅捷pdf转换器`转换的只是一张表内容，内容根本无法全覆盖多列内容，因为涉及好几个单元格的拼接，所以只好利用插件解析成数组对象，然后导出*

# 思路

1. 利用这个xslx包把excel表第一页解析成对象数组
2. 然后利用v-for遍历显示在html页面当中去
3. 导出.doc 文件

# 问题

1. 文档里必须经过修改首行字符为zh [已解决]
2. li标签导出出现错乱问题 [已解决]
3. 一开始认为导出文件直接 `ctrl-v` + `ctrl-c` 结果出现系统内存分配不足卡机，我也不知道是不是自己电脑配置方面落伍了，感觉应该是数据量太大，遍历占中CPU率太高，所以选择用`'data:application/vnd.ms-word;charset=utf-8,'`格式导出word文档  [已解决]

# 源文件

[点击下载](/file/《国际私法学》机考试题.xls)

# 源代码
```html
	<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
	<script type="text/javascript" src="https://unpkg.com/xlsx/dist/xlsx.full.min.js"></script>
	<div id="app">
		<input type="file" ref="upload" accept=".xls,.xlsx" class="outputlist_upload">
		<input type="text" name="" v-model="filename" style="text-align: center;"><span>.doc</span>
		<button type="button" @click="getOutword">导出word</button>
		<div id="downloadwrap">
			<ul>
				<div v-for="item in outputs" :key="item.id">
					<h4>{{item.id}}.&nbsp;{{item.title}}(&nbsp;)&nbsp;<small style="color: #999">[{{item.types}}]</small></h4>
					<p>A:{{item.a_select}}</p>
					<p>B:{{item.b_select}}</p>
					<p>C:{{item.c_select}}<p>
					<p>D:{{item.d_select}}</p>
					<div>
						正确答案：<font color="red">{{item.answer}}</font>
					</div>
				</div>
			</ul>
		</div>
	</div>
```
```javascript
		var vm = new Vue({
			el:'#app',
			data(){
				return{
					filename:'',
					outputs:[]
				}
			},
			mounted() {
			    this.$refs.upload.addEventListener('change', e => {//绑定监听表格导入事件
			    this.readExcel(e);
			    })
			},
			methods:{
				readExcel(e) {//表格导入
			        var that = this;
			        const files = e.target.files;
			        console.log(files);
			        if(files.length<=0){//如果没有文件名
			        return false;
			        }else if(!/\.(xls|xlsx)$/.test(files[0].name.toLowerCase())){
			        this.$Message.error('上传格式不正确，请上传xls或者xlsx格式');
			        return false;
			        }
			 
			        const fileReader = new FileReader();
			        fileReader.onload = (ev) => {
			        try {
			            const data = ev.target.result;
			            const workbook = XLSX.read(data, {
			            type: 'binary'
			            });
			            const wsname = workbook.SheetNames[0];//取第一张表
			            const ws = XLSX.utils.sheet_to_json(workbook.Sheets[wsname]);//生成json表格内容
			            console.log(ws);
			            that.outputs = [];//清空接收数据
			            for(var i= 0;i<ws.length;i++){
			            var sheetData = {
			            	types: ws[i].type,
			                id: ws[i].id,
			                title: ws[i].title,
			                a_select: ws[i].A,
			                b_select: ws[i].B,
			                c_select: ws[i].C,
			                d_select: ws[i].D,
			                answer: ws[i].answer,
			                dif: ws[i].dif,
			                name: ws[i].name

			            }
			            that.outputs.push(sheetData);
			            }
			            this.$refs.upload.value = '';
			 
			        } catch (e) {
			 
			            return false;
			        }
			        };
			        fileReader.readAsBinaryString(files[0]);
			    },
			    getOutword:function(id,fileName){
				  /*  id ：文档dom节点 fileName：文件名称(.doc) */
				  var header = "<html xmlns:o='urn:schemas-microsoft-com:office:office' " +
				    "xmlns:w='urn:schemas-microsoft-com:office:word' " +
				    "xmlns='http://www.w3.org/TR/REC-html40'>" +
				    "<head><meta charset='utf-8'><title>Export HTML to Word Document with JavaScript</title></head><body>"
				  var footer = '</body></html>'
				  var sourceHTML = header + document.getElementById('downloadwrap').innerHTML + footer
				 
				  var source = 'data:application/vnd.ms-word;charset=utf-8,' + encodeURIComponent(sourceHTML)
				  var fileDownload = document.createElement('a')
				  document.body.appendChild(fileDownload)
				  fileDownload.href = source
				  fileDownload.download = this.filename + '.doc' // 下载名称
				  fileDownload.click()
				  document.body.removeChild(fileDownload)
			    }
			},
		})
```
# 演示地址

<iframe src="/file/vue_excel.html" frameborder="0" width="100%" height="600px"></iframe>