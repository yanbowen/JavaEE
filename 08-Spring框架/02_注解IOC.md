## Spring的IOC的注解开发    
   
### Spring的IOC的注解开发的入门   
   
创建web项目，引入jar包
在Spring4的版本中，除了引入基本的开发包以外，还需要引入aop的包。   
   
![icon](img/02/img01-Spring.png)  
   
在src下创建applicationContext.xml   

* 引入约束：使用注解开发引入context约束
* spring-framework-5.0.7.RELEASE\docs\spring-framework-reference\index.html   

![icon](img/02/img02-Spring.png)    
  
开启Spring的组件扫描   
  
![icon](img/02/img03-Spring.png)   
   
在类上添加注解    
   
![icon](img/02/img04-Spring.png)   
    
   
编写测试类    
   
![icon](img/02/img05-Spring.png)    
   
  
### 注解方式设置属性的值
注解方式：使用注解方式，可以没有set方法的。   

* 属性如果有set方法，需要将属性注入的注解添加到set方法。
* 属性如果没有set方法，需要将属性注入的注解添加属性上。   

![icon](img/02/img06-Spring.png)    
  
  
### Spring的IOC的注解的详解
#### @Component：组件   
   
修饰一个类，将这个类交给Spring管理。  
这个注解有三个衍生注解（功能类似），修饰类。  

* @Controller	： web层
* @Service		： service层
* @Repository	： dao层   

  
### 属性注入的注解    

普通属性：   

* **@Value		：设置普通属性的值。**   
   
对象类型属性：     

* @Autowired	：设置对象类型的属性的值。但是按照**类型**完成属性注入。    
	* 我们习惯是按照名称完成属性注入：必须让@Autowired注解和@Qualifier一起使用完成按照名称属性注入。   
* **@Resource	：完成对象类型的属性的注入，按照名称完成属性注入。**   

![icon](img/02/img07-Spring.png)       
    
![icon](img/02/img08-Spring.png)   
   
  
### Bean的其他的注解   

生命周期相关的注解（了解）    

* @PostConstruct	：初始化方法
* @PreDestroy		：销毁方法    


Bean作用范围的注解   

* **@Scope			：作用范围**
	* **singleton	：默认单例**
	* **prototype	：多例**
	* request
	* session
	* globalsession   

  
单例模式  

![icon](img/02/img09-Spring.png)     
   
多例模式   
   
![icon](img/02/img10-Spring.png)     
  
![icon](img/02/img11-Spring.png)     
  
![icon](img/02/img12-Spring.png)     
     

### IOC的XML和注解开发比较
XML和注解的比较
适用场景    

* XML	：可以适用任何场景。
	* 结构清晰，维护方便。
* 注解：有些地方用不了，这个类不是自己提供的。
	* 开发方便。  

   
### 纯XML形式  
   
![icon](img/02/img13-Spring.png)  
  
![icon](img/02/img14-Spring.png)   
  
![icon](img/02/img15-Spring.png)    
  
![icon](img/02/img16-Spring.png)    
   
  
## Spring的AOP的XML开发
   
### AOP的概述   
   
AOP:面向切面编程。AOP是OOP的扩展和延伸，解决OOP开发遇到问题。   
   
### Spring底层的AOP实现原理   
  
动态代理   

* JDK动态代理			：只能对实现了接口的类产生代理。
* Cglib动态代理（类似于Javassist第三方代理技术）：对没有实现接口的类产生代理对象。生成子类对象。   

  
![icon](img/02/img17-Spring.png)      
   
### Spring的AOP底层实现（了解）   
   
#### JDK动态代理   
   
![icon](img/02/img18-Spring.png)      
   
![icon](img/02/img19-Spring.png)      
   
![icon](img/02/img20-Spring.png)      
   
![icon](img/02/img21-Spring.png)      
     

### Cglib动态代理   
   
Cglib：第三方开源代码生成类库，动态添加类的属性和方法。    
   
![icon](img/02/img22-Spring.png)     
  
![icon](img/02/img23-Spring.png)     
   
![icon](img/02/img24-Spring.png)     
   
  
## Spring的AOP的开发（AspectJ的XML的方式）   
   
### Spring的AOP的简介    
  
AOP思想最早是由AOP联盟组织提出的。Spring使用这种思想最好的框架。   

* Spring的AOP有自己实现的方式（非常繁琐）。AspectJ是一个AOP的框架，Spring引入AspectJ作为自身AOP的开发。
* Spring两套AOP开发方式
	* Spring传统方式（弃用）。
	* Spring基于AspectJ的AOP的开发（使用）。   

  
![icon](img/02/img25-Spring.png)     
     
### 创建web项目，引入jar包
引入基本开发包   
引入aop开发的相关jar包
   
![icon](img/02/img26-Spring.png)    
   
### 引入Spring的配置文件    
   
引入aop的约束   
   
![icon](img/02/img27-Spring.png)    
   
编写目标类并完成配置    
   
![icon](img/02/img28-Spring.png)    
   
编写测试类：    
  
![icon](img/02/img29-Spring.png)    
   
编写一个切面类    
   
![icon](img/02/img30-Spring.png)    
   
将切面类交给Spring   
  
![icon](img/02/img31-Spring.png)     
   
通过AOP的配置实现    
   
![icon](img/02/img32-Spring.png)     
       
   
## Spring中通知类型    
    
### 前置通知：在目标方法执行之前进行操作    
  
前置通知：获得切入点信息      
![icon](img/02/img33-Spring.png)      

   
### 后置通知：在目标方法执行之后进行操作     
   
后置通知：获得方法的返回值。    
![icon](img/02/img34-Spring.png)       

![icon](img/02/img35-Spring.png)      
   
![icon](img/02/img36-Spring.png)   
    
   
### 环绕通知：在目标方法执行之前和之后进行操作    
    
环绕通知可以阻止目标方法的执行    
![icon](img/02/img37-Spring.png)       
   
![icon](img/02/img38-Spring.png)      
  
![icon](img/02/img39-Spring.png)      
   
![icon](img/02/img40-Spring.png)   
   
### 异常抛出通知：在程序出现异常的时候，进行的操作    
      
![icon](img/02/img41-Spring.png)    
    
![icon](img/02/img42-Spring.png)   
   
![icon](img/02/img43-Spring.png)      
   
   
### 最终通知：无论代码是否有异常，总是会执行     
    
   
### Spring的切入点表达式写法：   
   
语法   

	[访问修饰符] 方法返回值 包名.类名.方法名(参数)
	public void com.swust.spring.CustomerDao.save(..)
	* *.*.*.* Dao.save(..)
	* com.swust.spring.CustomerDao+.save(..)
	* com.swust.spring..*.*(..)