<center>  

# javaEE框架师之路  

<hr width = "50%">  

## 二、CSS & javaScript    

</center>     
   
![](https://i.imgur.com/mka0K21.png)   
   
#### HTML的块标签:  

* div标签：默认占一行,自动换行  
* span标签：内容显示在同一行

#### Cascading Style Sheets : 层叠样式表（CSS）   
   
CSS语法:在一个style标签中,去编写CSS内容,最好将style标签写在这个head标签中   
   
	<style>
	  选择器{
	    属性名称:属性的值;
	    属性名称2: 属性的值2;
	  }
	</style>   
     

元素选择:

	元素的名称{
	  属性名称:属性的值;
	  属性名称:属性的值;
	}

ID选择器:

	以#号开头  ID在整个页面中必须是唯一的s
	#ID的名称{
	  属性名称:属性的值;
	  属性名称:属性的值;
	}

类选择器:

	以 . 开头 
	.类的名称{
		属性名称:属性的值;
		属性名称:属性的值;
	}    
     
	<style>
		.shuiguo{
			color: yellow;
		}
		.shucai{
			color: green;
		}
	</style>

	<div class="shucai">茄子</div>
	<div class="shuiguo">橘子</div>   
   
CSS的引入方式:

​外部样式: 通过link标签引入一个外部的css文件   

	<link rel="stylesheet" href="style1.css" />

​内部样式: 直接在style标签内编写CSS代码   


​行内样式: 直接在标签中添加一个style属性, 编写CSS样式   
  
	<div class="shuiguo" style="color: greenyellow;">甘蔗</div>    
    
#### CSS浮动 : 浮动的元素会脱离正常的文档流,在正常的文档流中不占空间   

	float属性:
		left
		right
					
	clear属性: 清除浮动
		both : 两边都不允许浮动
		left: 左边不允许浮动
		right : 右边不允许浮动
	流式布局   
    
#### CSS的盒子模型: 万物皆盒子

	内边距:  
	
	padding-top:
	padding-right:
	padding-bottom:
	padding-left:   
   
	外边距:
	
	margin-top:
	margin-right:
	margin-bottom:
	margin-left:   
     
  
---  

### JavaScript概述

什么是脚本语言?

​	java源代码 ----> 编译成.class文件 -----> java虚拟机中才能执行

​	脚本语言:   源码  -------- > 解释执行

​	js由我们的浏览器来解释执行   
   
     
### 轮播图自动播放  

- 定时器
  - setInterval : 每隔多少毫秒执行一次函数
  - setTimeout: 多少毫秒之后执行一次函数
  - clearInterval
  - clearTimeout
- 显示广告 img.style.display  = "block"
- 隐藏广告 img.style.display  = "none"    

	    <script>
	
	        function init() {
	            setTimeout("showAD()", 3000);
	        }
	
	        function showAD() {
	            //首先要获取要操作的img
	            var img = document.getElementById("img1");
	            //显示广告
	            img.style.display = "block";
	
	            //再开启定时器,关闭广告
	            setTimeout("hideAD()", 3000);
	        }
	
	        function hideAD() {
	            //首先要获取要操作的img
	            var img = document.getElementById("img1");
	            //隐藏广告
	            img.style.display = "none";
	        }
	    </script>    
    
【JS中的常用事件】

onfocus 事件: 获得焦点事件

onblur : 失去焦点

onkeyup : 按键抬起事件     
     
【HTML中的DOM操作】 --- DOM: Document Object Model


	一些常用的 HTML DOM 方法：
	  getElementById(id) - 获取带有指定 id 的节点（元素） 
	  appendChild(node) - 插入新的子节点（元素） 
	  removeChild(node) - 删除子节点（元素） 
	
	  一些常用的 HTML DOM 属性：
	  innerHTML - 节点（元素）的文本值 
	  parentNode - 节点（元素）的父节点 
	  childNodes - 节点（元素）的子节点 
	  attributes - 节点（元素）的属性节点 
	
	
	查找节点：
	getElementById() 返回带有指定 ID 的元素。 
	getElementsByTagName() 返回包含带有指定标签名称的所有元素的节点列表（集合/节点数组）。 
	getElementsByClassName() 返回包含带有指定类名的所有元素的节点列表。 
	
	增加节点：
	createAttribute() 创建属性节点。 
	createElement() 创建元素节点。 
	createTextNode() 创建文本节点。 
	insertBefore() 在指定的子节点前面插入新的子节点。 
	appendChild() 把新的子节点添加到指定节点。 
	
	删除节点：
	removeChild() 删除子节点。 
	replaceChild() 替换子节点。 
	
	修改节点：
	setAttribute()  修改属性
	setAttributeNode()  修改属性节点   
   
