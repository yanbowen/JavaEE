# Ajax & Jquery

## Ajax

* 是什么?

> “Asynchronous Javascript And XML”（异步JavaScript和XML），

> 并不是新的技术，只是把原有的技术，整合到一起而已。 

		   1.使用CSS和XHTML来表示。
		   2. 使用DOM模型来交互和动态显示。
		   3.使用XMLHttpRequest来和服务器进行异步通信。
		   4.使用javascript来绑定和调用。

* 有什么用?

> 咱们的网页如果想要刷新局部内容。 那么需要重新载入整个网页。用户体验不是很好。  就是为了解决局部刷新的问题。 保持其他部分不动，只刷新某些地方。 
  
## 数据请求 Get

	1.创建对象

			function  ajaxFunction(){
			   var xmlHttp;
			   try{ // Firefox, Opera 8.0+, Safari
			        xmlHttp=new XMLHttpRequest();
			    }
			    catch (e){
				   try{// Internet Explorer
				         xmlHttp=new ActiveXObject("Msxml2.XMLHTTP");
				      }
				    catch (e){
				      try{
				         xmlHttp=new ActiveXObject("Microsoft.XMLHTTP");
				      }
				      catch (e){}
				      }
			    }
				return xmlHttp;
			 }

	2. 发送请求

		//执行get请求
		function get() {
			
			//1. 创建xmlhttprequest 对象
			var request = ajaxFunction();
			
			//2. 发送请求。
			// http://localhost:8080/day16/demo01.jsp
			//http://localhost:8080/day16/DemoServlet01
			
			/*	
				参数一： 请求类型  GET or  POST
				参数二： 请求的路径
				参数三： 是否异步， true  or false
			*/
			request.open("GET" ,"/day16/DemoServlet01" ,true );
			request.send();
		}


	如果发送请求的同时，还想获取数据，那么代码如下
	
		//执行get请求
		function get() {
			
			//1. 创建xmlhttprequest 对象
			var request = ajaxFunction();
			
			//2. 发送请求
			request.open("GET" ,"/day16/DemoServlet01?name=aa&age=18" ,true );
			
			//3. 获取响应数据 注册监听的意思。  一会准备的状态发生了改变，那么就执行 = 号右边的方法
			request.onreadystatechange = function(){
				
				//前半段表示 已经能够正常处理。  再判断状态码是否是200
				if(request.readyState == 4 && request.status == 200){
					//弹出响应的信息
					alert(request.responseText);
				}
			}
			request.send();
		}


## 数据请求 Post

	<script type="text/javascript">
		//1. 创建对象
		function  ajaxFunction(){
		   var xmlHttp;
		   try{ // Firefox, Opera 8.0+, Safari
		        xmlHttp=new XMLHttpRequest();
		    }
		    catch (e){
			   try{// Internet Explorer
			         xmlHttp=new ActiveXObject("Msxml2.XMLHTTP");
			      }
			    catch (e){
			      try{
			         xmlHttp=new ActiveXObject("Microsoft.XMLHTTP");
			      }
			      catch (e){}
			      }
		    }
		
			return xmlHttp;
		 }
		
		function post() {
			//1. 创建对象
			var request = ajaxFunction();
			
			//2. 发送请求
			request.open( "POST", "/day16/DemoServlet01", true );
		
			//如果不带数据，写这行就可以了
			//request.send();
			
			//如果想带数据，就写下面的两行
			
			//如果使用的是post方式带数据，那么 这里要添加头， 说明提交的数据类型是一个经过url编码的form表单数据
			request.setRequestHeader("Content-type","application/x-www-form-urlencoded");
			
			//带数据过去  ， 在send方法里面写表单数据。 
			request.send("name=aobama&age=19");
		}
	</script>


	需要获取数据

		function post() {
			//1. 创建对象
			var request = ajaxFunction();
			
			//2. 发送请求
			request.open( "POST", "/day16/DemoServlet01", true );
			
			//想获取服务器传送过来的数据， 加一个状态的监听。 
			request.onreadystatechange=function(){
				if(request.readyState==4 && request.status == 200){
					
					alert("post："+request.responseText);
				}
			}
			
			//如果使用的是post方式带数据，那么 这里要添加头， 说明提交的数据类型是一个经过url编码的form表单数据
			request.setRequestHeader("Content-type","application/x-www-form-urlencoded");
			
			//带数据过去  ， 在send方法里面写表单数据。 
			request.send("name=aobama&age=19");
		}

## 校验用户名是否可用

### 1. 搭建环境

1. 页面准备

   	<body>
   	<table border="1" width="500">
   		<tr>
   			<td>用户名:</td>
   			<td><input type="text" name="name" id="name"  onblur="checkUserName()"><span id="span01"></span></td> 
   		</tr>
   		<tr>
   			<td>密码</td>
   			<td><input type="text" name=""></td>
   		</tr>
   		<tr>
   			<td>邮箱</td>
   			<td><input type="text" name=""></td>
   		</tr>
   		<tr>
   			<td>简介</td>
   			<td><input type="text" name=""></td>
   		</tr>
   		<tr>
   			<td colspan="2"><input type="submit" value="注册"></td>
   		</tr>
   	</table>
   </body>


2. 数据库准备

### 2. Servlet代码

		protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		try {
			
			request.setCharacterEncoding("UTF-8");
			
			//1. 检测是否存在
			String name = request.getParameter("name");
			System.out.println("name="+name);
			
			UserDao dao = new UserDaomImpl();
			boolean isExist = dao.checkUserName(name);
			
			//2.  通知页面，到底有还是没有。
			if(isExist){
				response.getWriter().println(1);  //存在用户名
			}else{
				response.getWriter().println(2); //不存在该用户名
			}
			
		} catch (SQLException e) {
			e.printStackTrace();
		}
	}

### 3. Dao代码


		public class UserDaomImpl implements UserDao{

			@Override
			public boolean checkUserName(String username) throws SQLException {
				QueryRunner runner = new QueryRunner(JDBCUtil02.getDataSource());
				
				String sql = "select count(*) from t_user where username =?";


				runner.query(sql, new  ScalarHandler(), username);

				Long result = (Long) runner.query(sql, new  ScalarHandler(), username); 
				return result > 0 ;
			}
		
		}

### jsp页面显示


​		
	function checkUserName() {

		//获取输入框的值 document 整个网页
		var name = document.getElementById("name").value; // value  value() val val()
		//1. 创建对象
		var request = ajaxFunction();
		
		//2. 发送请求
		request.open("POST"  ,"/day16/CheckUserNameServlet" , true );
		
		//注册状态改变监听，获取服务器传送过来的数据
		request.onreadystatechange = function(){
			
			if(request.readyState == 4 && request.status == 200){
				//alert(request.responseText);
				var data = request.responseText;
				if(data == 1){
					//alert("用户名已存在");
					document.getElementById("span01").innerHTML = "<font color='red'>用户名已存在!</font>";
				}else{
					document.getElementById("span01").innerHTML = "<font color='green'>用户名可用!</font>";
					//alert("用户名未存在");
				}
			}
			
		}
		
		request.setRequestHeader("Content-type","application/x-www-form-urlencoded");
		request.send("name="+name);
	}
