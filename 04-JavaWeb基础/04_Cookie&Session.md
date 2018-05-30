## 中文文件下载

> 针对浏览器类型，对文件名字做编码处理 Firefox (Base64) , IE、Chrome ... 使用的是URLEncoder

		/*
		 * 如果文件的名字带有中文，那么需要对这个文件名进行编码处理
		 * 如果是IE ，或者  Chrome （谷歌浏览器） ，使用URLEncoding 编码
		 * 如果是Firefox ， 使用Base64编码
		 */
		//获取来访的客户端类型
		String clientType = request.getHeader("User-Agent");
		
		if(clientType.contains("Firefox")){
			fileName = DownLoadUtil.base64EncodeFileName(fileName);
		}else{
			//IE ，或者  Chrome （谷歌浏览器） ，
			//对中文的名字进行编码处理
			fileName = URLEncoder.encode(fileName,"UTF-8");
		}
   
## 请求转发和重定向

### 重定向

			/*
			之前的写法
			response.setStatus(302);
			response.setHeader("Location", "login_success.html");*/
			
			//重定向写法： 重新定位方向 参数即跳转的位置
		response.sendRedirect("login_success.html");

		1. 地址上显示的是最后的那个资源的路径地址

		2. 请求次数最少有两次， 服务器在第一次请求后，会返回302 以及一个地址， 浏览器在根据这个地址，执行第二次访问。

		3. 可以跳转到任意路径。 不是自己的工程也可以跳。

		4. 效率稍微低一点， 执行两次请求。 

		5. 后续的请求，没法使用上一次的request存储的数据，或者 没法使用上一次的request对象，因为这是两次不同的请求。

### 请求转发

		//请求转发的写法： 参数即跳转的位置
		request.getRequestDispatcher("login_success.html").forward(request, response);

		1. 地址上显示的是请求servlet的地址。  返回200 ok

		2. 请求次数只有一次， 因为是服务器内部帮客户端执行了后续的工作。 

		3. 只能跳转自己项目的资源路径 。  

		4. 效率上稍微高一点，因为只执行一次请求。 

		5. 可以使用上一次的request对象。 

## Cookie

> 饼干. 其实是一份小数据， 是服务器给客户端，并且存储在客户端上的一份小数据

### 应用场景

> 自动登录、浏览记录、购物车。

### 为什么要有这个Cookie

> http的请求是无状态。 客户端与服务器在通讯的时候，是无状态的，其实就是客户端在第二次来访的时候，服务器根本就不知道这个客户端以前有没有来访问过。 为了更好的用户体验，更好的交互 [自动登录]，其实从公司层面讲，就是为了更好的收集用户习惯[大数据]

### Cookie怎么用  
  
#### 简单使用：

* 添加Cookie给客户端

	1. 在响应的时候，添加cookie
		
			Cookie cookie = new Cookie("aa", "bb");
			
			//给响应，添加一个cookie
			response.addCookie(cookie);

	2. 客户端收到的信息里面，响应头中多了一个字段 Set-Cookie
	3. ![icon](img/img02-Cookie.png)

* 获取客户端带过来的Cookie

		//获取客户端带过来的cookie
		Cookie[] cookies = request.getCookies();
		if(cookies != null){
			for (Cookie c : cookies) {
				String cookieName = c.getName();
				String cookieValue = c.getValue();
				System.out.println(cookieName + " = "+ cookieValue);
			}
		}

* 常用方法

		//关闭浏览器后，cookie就没有了。 ---> 针对没有设置cookie的有效期。
		//	expiry： 有效 以秒计算。
		//正值 ： 表示 在这个数字过后，cookie将会失效。
		//负值： 关闭浏览器，那么cookie就失效， 默认值是 -1
		cookie.setMaxAge(60 * 60 * 24 * 7);
		
		//赋值新的值
		//cookie.setValue(newValue);
		
		//用于指定只有请求了指定的域名，才会带上该cookie
		cookie.setDomain(".itheima.com");
		
		//只有访问该域名下的cookieDemo的这个路径地址才会带cookie
		cookie.setPath("/CookieDemo");   
   
###Jsp 里面使用Java代码

* jsp

> Java Server Pager ---> 最终会翻译成一个类， 就是一个Servlet

* 定义全局变量

	<%! int a = 99; %>

* 定义局部变量

	<% int b = 999; %>
	
* 在jsp页面上，显示 a 和 b的值，
 
	<%=a %> 
	<%=b %>

###jsp显示浏览记录

![icon](img/img04-Jsp.png)   
   
#Session

> 会话 ， Session是基于Cookie的一种会话机制。 Cookie是服务器返回一小份数据给客户端，并且存放在客户端上。 Session是，数据存放在服务器端。


* 常用API


		//得到会话ID
		String id = session.getId();
		
		//存值
		session.setAttribute(name, value);
		
		//取值
		session.getAttribute(name);
		
		//移除值
		session.removeAttribute(name);

* Session何时创建，何时销毁?

* 创建

> 如果有在servlet里面调用了 request.getSession()

* 销毁

> session 是存放在服务器的内存中的一份数据。 当然可以持久化. Redis . 即使关了浏览器，session也不会销毁。

> 1. 关闭服务器

> 2. session会话时间过期。 有效期过了，默认有效期： 30分钟。    

### 移除Session中的元素

		在jsp中<% %> 写
		//强制干掉会话，里面存放的任何数据就都没有了。
		session.invalidate();
		
		//从session中移除某一个数据
		//session.removeAttribute("cart");