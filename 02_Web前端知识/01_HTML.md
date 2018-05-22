<center>  

# javaEE框架师之路  

<hr width = "50%">  

## 二、HTML    

</center>    
     
### HTML: Hyper Text Markup Language 超文本标记语言
  
	<h1>静夜诗</h1>
	<b><i>--李白</i> </b> <br/>
	<p>床前明月光,</p>
	<p>地上鞋两双,</p>
	<p>举头望明月,</p>
	<p>低头思故乡.</p>   
       
   
代码分析  
   
	<html>
		<head>
			<meta charset="UTF-8">
			<title>网站信息页面</title>
		</head>
		<body>
			<!--
				1. 公司简介 需要标题
				2. 水平分割线
				3. 四个段落
				4. 第一个段落字体需要红色
			-->
			<h3>公司简介</h3>
			
			<hr />
			<p>
			<font color="red">“中关村黑马程序员训练营”</font>是由<b><i>传智播客</i></b>联合中关村软件园、CSDN，并委托传智播客进行教学实施的软件开发高端培训机构，致力于服务各大软件企业，解决当前软件开发技术飞速发展，而企业招不到优秀人才的困扰。 目前，“中关村黑马程序员训练营”已成长为行业“学员质量好、课程内容深、企业满意”的移动开发高端训练基地，并被评为中关村软件园重点扶持人才企业。
			</p>
			<p>
			<strong>黑马程序员</strong>的学员多为大学毕业后，<em>有理想、有梦想，</em>想从事IT行业，而没有环境和机遇改变自己命运的年轻人。黑马程序员的学员筛选制度，远比现在90%以上的企业招聘流程更为严格。任何一名学员想成功入学“黑马程序员”，必须经历长达2个月的面试流程，这些流程中不仅包括严格的技术测试、自学能力测试，还包括性格测试、压力测试、品德测试等等测试。毫不夸张地说，黑马程序员训练营所有学员都是精挑细选出来的。百里挑一的残酷筛选制度确保学员质量，并降低企业的用人风险。
			</p>
			<p>
			中关村黑马程序员训练营不仅着重培养学员的基础理论知识，更注重培养项目实施管理能力，并密切关注技术革新，不断引入先进的技术，研发更新技术课程，确保学员进入企业后不仅能独立从事开发工作，更能给企业带来新的技术体系和理念。
			</p>
			<p>
			一直以来，黑马程序员以技术视角关注IT产业发展，以深度分享推进产业技术成长，致力于弘扬技术创新，倡导分享、 开放和协作，努力打造高质量的IT人才服务平台。
			</p>
		</body>
	</html>  

#### 扩展内容

	b : 加粗
	i : 斜体
	strong: 加粗, 带语义标签
	em:  斜体, 带语义   

----
	<!DOCTYPE html>
	<html>
		<head>
			<meta charset="UTF-8">
			<title></title>
		</head>
		<body>
			<!--
				常用属性:
					src : 指定图片路径
					width : 指定图片宽度
					height : 图片高度
					alt : 文件加载失败时的提示信息
			-->
			<img src="../img/美女22.jpg" width="500px" alt="这张图片可能加载问题" />
		</body>
	</html>
	
	
	<!DOCTYPE html>
	<html>
		<head>
			<meta charset="UTF-8">
			<title></title>
		</head>
		<body>
			<!--在网页中显示图片-->
			<img src="../img/logo2.png" width="30%"/>
			<img src="../image/header.jpg" width="30%" />
		</body>
	</html>
   
---   
   
#### 列表标签: 

	​无序列表:  ul
	​	type: 小圆圈,小圆点, 小方块
	​有序列表: ol
	​	type: 1,a ,A,I,
	​	start : 指定是起始索引   

---  
   
	<!DOCTYPE html>
	<html>
		<head>
			<meta charset="UTF-8">
			<title></title>
		</head>
		<!--
			1.使用无序列表
				百合网
				世纪家园
				珍爱网
				非诚勿扰
		-->
		<body>
			<ul>
				<li><a href="http://www.baihe.com" target="_blank">百合网</a></li>
				<li><a href="http://www.jiayuan.com">世纪家园</a></li>
				<li>珍爱网</li>
				<li>非诚勿扰</li>
			</ul>
		</body>
	</html>   
   
	点击链接,跳转去指定网站

#### a 超链接标签  

	常用的属性:  
	
	href: 指定要跳转去的链接地址    
		- 如果是网络地址需要加上http协议 
		- 如果访问的是本网站的html文件,可以直接写文件路径
		
	target : 以什么方式打开  	
		_self: 默认打开方式,在当前窗口打开
		_blank:  新起一个标签页打开页面    
    
####  表格标签table

	table标签:  
		tr 行  td 列	
		bgcolor : 背景色
		width : 	宽度
		height : 高度
		align : 对齐方式

#### 合并单元格:

	​colspan : 跨列操作
	​rowspan : 跨行操作
	
	​注意: 跨行或者跨列操作之后,被占掉的格子需要删除掉   
  
----   
   
	<form action="../04-网站首页/网站首页.html" method="post">
	    <!--隐藏域
	        主要是用来存放页面上一些ID信息
	    -->
	    <input type="hidden" value="sadfaldsfkjl@o3214813278" name="uid"/>
	    <!--文本输入框-->
	    用户名: <input type="text" name="username" id="username" placeholder="请输入用户名"/><br/>
	    <!--密码框-->
	    密码: <input type="password" placeholder="请输入密码"/> <br/>
	    确认密码: <input type="password"/> <br/>
	    邮箱: <input type="text"/> <br/>
	
	    手机号码: <input type="tel"/> <br/>
	    靓照: <input type="file"/> <br/>
	
	    性别: <input type="radio" name="sex"/>男
	    <input type="radio" name="sex"/>女
	    <input type="radio" name="sex"/>妖 <br/>
	
	    爱好:
	    <input type="checkbox"/>抽烟
	    <input type="checkbox"/>喝酒
	    <input type="checkbox"/>烫头
	    <input type="checkbox"/>撸代码
	    <input type="checkbox"/>大宝剑
	    <br/>
	
	    择偶要求:
	    <textarea cols="40" rows="4"></textarea><br/>
	    籍贯 :
	    <select>
	        <option>--请选择--</option>
	        <option>湖北</option>
	        <option>内蒙古</option>
	        <option>火星</option>
	    </select>
	
	    <br/>
	    出生日期:
	    <input type="datetime-local"/> <br/>
	    验证码: <input type="text"/><br/>
	
	    <input type="submit" value="注册"/>
	    <input type="button" value="普通按钮"/>
	    <input type="reset" value="重置按钮"/>
	</form>     
   
![](https://i.imgur.com/VoaqkIH.png)    
   
