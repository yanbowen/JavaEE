<center>  

# javaEE框架师之路  

<hr width = "50%">  

## 三、jQuery & BootStrap  

</center>     
   
jQuery是一个快速、简洁的JavaScript框架  
  
![](https://i.imgur.com/jkUSZMr.png)
    
	<!DOCTYPE html>
	<html>
		<head>
			<meta charset="UTF-8">
			<link rel="stylesheet" href="../css/style.css" />
			<title></title>
			<!--
				1. 首先给必填项,添加尾部添加一个小红点
				2. 获取用户输入的信息,做相应的校验
				3. 事件: 获得焦点, 失去焦点, 按键抬起
				4. 表单提交的事件
				
				Jq的方式来实现:
					1. 导入JQ的文件
					2. 文档加载事件: 在必填项后天加一个小红点
					3. 表单校验确定事件: blur focus keyup
					4. 提交表单 submit
			-->
			<script type="text/javascript" src="../js/jquery-1.11.0.js" ></script>
			<script>
				
				$(function(){  //默认做一些页面初始化
					//动态在必填项后面添加小红点
					$(".bitian").after("<font class='high'>*</font>");
					
					//给必填项绑定事件
					$(".bitian").blur(function(){
						//首先获取用户当前输入的值
						var value = this.value; //123
						//清空上一次提示的信息
						$(this).parent().find(".formtips").remove();
						
						//判断当前的值是哪一项输入的值
						if($(this).is("#username")){  //判断是否是用户名输入项
							if(value.length < 6){
								$(this).parent().append("<span class='formtips onError'>用户名太短了</span>");
							}else{
								$(this).parent().append("<span class='formtips onSuccess'>用户名够用</span>");
							}
						}
						
						if($(this).is("#password")){  //判断是否是密码输入项
							if(value.length < 6){
								$(this).parent().append("<span class='formtips onError'>,密码太短了</span>");
							}else{
								$(this).parent().append("<span class='formtips onSuccess'>密码够用</span>");
							}
						}
					}).focus(function(){
						$(this).triggerHandler("blur");
					}).keyup(function(){
						$(this).triggerHandler("blur");
					})
					
					
					
					//给表单提交绑定事件
					$("form").submit(function(){
						//触发所有必填项的校验
						$(".bitian").trigger("focus");
						//找到错误信息的个数
						if($(".onError").length > 0){
							return false;
						}
						return true;
					});
				});
				
				
				
				
				
				
				
			/*	
				$(function(){
					// 在所有必填项后天加一个小红点 *
					$(".bitian").after("<font class='high'>*</font>");
					
					//事件绑定
					$(".bitian").blur(function(){
	//					var value = this.value;
						var value = $(this).val();
						//清空当前必填项后面的span 
	//					$(".formtips").remove();
						$(this).parent().find(".formtips").remove();
						//获得当前事件是谁的
						if($(this).is("#username")){
							//校验用户名
							if(value.length < 6){
								$(this).parent().append("<span class='formtips onError'>用户名太短了</span>");
							}else{
								$(this).parent().append("<span class='formtips onSuccess'>用户名够用</span>");
							}
						}
						
						if($(this).is("#password")){
							//校验密码
							if(value.length < 3){
								$(this).parent().append("<span class='formtips onError'>密码太短了</span>");
							}else{
								$(this).parent().append("<span class='formtips onSuccess'>密码够用</span>");
							}
						}
					}).focus(function(){
						$(this).triggerHandler("blur");
					}).keyup(function(){
						$(this).triggerHandler("blur");
					});
					
	//				$(".bitian").blur(function(){}).focus(function(){}).keyup(function(){})
	
					//给表单绑定提交事件
					$("form").submit(function(){
						//触发必填项的校验逻辑
						$(".bitian").trigger("focus");
						
						var length = $(".onError").length
						if(length > 0){
							return false;
						}
						return true;
					});
				});*/
				
			</script>
		</head>
		<body>
			<form action="../index.html">
				<div>
					用户名:<input type="text" class="bitian" id="username" />
				</div>
				<div>
					密码:<input type="password"  class="bitian" id="password" />
				</div>
				<div>
					手机号:<input type="tel" />
				</div>
				<div>
					<input type="submit" />
				</div>
			</form>
		</body>
	</html>
      
---  

### BootStrap

Bootstrap 是基于 HTML、CSS、JavaScript 的，它简洁灵活，使得 Web 开发更加快捷。
   
- BootStrap有什么作用
  - 复制粘贴, 能够提高开发人员的工作效率


- 什么是响应式页面
  - 适应不同的分辨率显示不同样式,提高用户的体验   

- BootStrap的中文网
  - http://www.bootcss.com    

#### BootStrap的入门开发

- 引入相关的头文件

		<!-- 最新版本的 Bootstrap 核心 CSS 文件 -->
		<link rel="stylesheet" href="../css/bootstrap.css" />
		
		<!--需要引入JQuery-->
		<script type="text/javascript" src="../js/jquery-1.11.0.js" ></script>
		
		<!-- 最新的 Bootstrap 核心 JavaScript 文件 -->
		<script type="text/javascript" src="../js/bootstrap.js" ></script>
		
		<meta name="viewport" content="width=device-width, initial-scale=1">   
   
- BootStrap的布局容器

		.container 类用于固定宽度并支持响应式布局的容器。
		<div class="container">
		  ...
		</div>
		

		.container-fluid 类用于 100% 宽度，占据全部视口（viewport）的容器。		
		<div class="container-fluid">
		  ...
		</div>   
     
#### 栅格系统
Bootstrap 提供了一套响应式、移动设备优先的流式栅格系统，随着屏幕或视口（viewport）尺寸的增加，系统会自动分为最多12列。   

		<!DOCTYPE html>
		<html>
		
		<head>
		    <meta charset="UTF-8">
		    <title></title>
		
		    <!-- 最新版本的 Bootstrap 核心 CSS 文件 -->
		    <link rel="stylesheet" href="../css/bootstrap.css"/>
		
		    <!--需要引入JQuery-->
		    <script type="text/javascript" src="../js/jquery-1.11.0.js"></script>
		
		    <!-- 最新的 Bootstrap 核心 JavaScript 文件 -->
		    <script type="text/javascript" src="../js/bootstrap.js"></script>
		
		    <meta name="viewport" content="width=device-width, initial-scale=1">
		
		    <style>
		        div{
		            border: 1px solid red;
		        }
		    </style>
		</head>
		
		<body>
		<div class="container">
		    <a href="#" class="btn btn-warning">百合网</a>
		    <a href="#">世纪佳缘</a>
		
		    <div class="row">
		
		        <div class="col-md-8 col-sm-8">
		            123
		        </div>
		        <div class="col-md-5 col-sm-5">
		            456
		        </div>
		
		    </div>
		</div>
		
		</body>
		
		</html>   
   
---    
   
