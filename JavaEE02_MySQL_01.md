<center>  

# javaEE框架师之路  

<hr width = "50%">  

## 三、MySQL（Structured Query Language）    

</center>    
     
### 常见服务器  
   
关系型数据库：是建立在关系模型基础上的数据库，借助于集合代数等数学概念和方法来处理数据库中的数据   

* mariadb ： MariaDB数据库管理系统是MySQL的一个分支，主要由开源社区在维护，采用GPL授权许可 MariaDB的目的是完全兼容MySQL，包括API和命令行，使之能轻松成为MySQL的代替品。   
* db2 ： IBM公司，解决方案和硬件   
* oracle ： 甲骨文   
* sqlserver ： Windows使用，政府网站，（ASP.net）(图形化工具不错)  
* sybase ： 被淘汰   

非关系型数据库： key - value形式   

* MongoDB   
* Redis    
      
### 常用命令   
mysql -u root -proot   
   
![](https://i.imgur.com/C6X0i3w.png)   
   

   
	// 创建数据库
	create database mydatabase;
	// 创建数据库 并制定字符集
	create database mydatabase set utf8;    
   
##详细见 Android 15-day  16-day    
   
	create database 数据库名   
	   
	create table 表名(
		列名   列的类型(长度)  约束，
		列名2  列的类型(长度)  约束
	);   
   
	列的类型：  
	java			sql  
	int				int
	char/string		char/varchar		
					char:固定长度，varchar: 可变长度
	
	date			date	  ：	 YYYY-MM-DD
					time	  ：	 hh:mm:ss
					datetime  ：	 YYYY-MM-DD hh:mm:ss 默认值是null
					timestamp ：	 YYYY-MM-DD hh:mm:ss 默认使用当前时间   

					text	  ：	 存放文本
					blob	  ：	 存放的是二进制   

	   
	列的约束：
		主键约束： primary key
		唯一约束： unique
		非空约束： not null   
   
### 查看表  
   
	// 查看所有的表
	show tables;  
	
	show create table student;
	// 查看表结构
	desc student;
	
### 修改表  
  
	//添加表（add）
	alter table 表名 add 列名 列的类型 列的约束
	alter table student add chengji int not null
	//修改列（modify）
	alter table student modify sex varchar(2);
  
	//修改列名（change）  
	alter table student change sex gender varchar(2);
	//删除列（drop）
	alter table student drop chengji;
  
	//修改表名
	rename table student to students;
	//修改字符集
	alter table students character set utf8;  
		
### 删除表   
   
	drop table sutdents; 
    
![](https://i.imgur.com/vgECnm2.png)   
    
