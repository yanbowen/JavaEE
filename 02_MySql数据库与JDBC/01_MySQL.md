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
    
   
### sql完成对表中数据的CRUD的操作   
  
#### 插入数据  
  
	insert into 表名(列名1，列名2，列名3) values（值1，值2，值3）；  
	  
	insert into student(sid,sname,sex,age) values(1,'zhangsan',1,23);   
	//简单写法   
	insert into student values(1,'zhangsan',1,23);  
	   
	//查看表中数据
	select * from student   
   
#### 批量插入   
   
	insert into student values(2,'lisi',2,34),(4,'wanger',1,35),(5,'chenge',2,56);   
   
#### 删除记录  
   
	delete from 表名 [where 条件]  
	
	delete from student where sid = 3;
	delete frome student;全部删除   
   
#### 面试题： delete 删除与 truncate 删除数据有什么区别？	
  
	delete ： DML 一条条删除表中的数据，
	truncate ： DDL 先删除表再重建表；   
	那个方法效率高呢，具体情况而定，表中数据少，delete高，数据多，truncate 高；    
   
#### 更新表记录   
    
	update 表名 set 列名=列的值，列名2=列的值2 [where 条件]  
	
	update student set sname='周瑜' where sid = 5;  
	无条件全部更改表中数据  
	  
#### 查询记录   
   
	select [distinct] [*] [列名，列名2] from 表名 [where 条件] 
	distinct ： 去除重复数据   
  
	create table category(
		cid int primary key auto_increment,
		cname varchar(10),
		cdesc varchar(30)
	);
	
	insert into category values(null,'手机数码','电子产品');
	insert into category values(null,'鞋靴箱包','江南皮革厂');
	insert into category values(null,'香烟酒水','黄鹤楼，茅台');
	insert into category values(null,'馋嘴零食','八宝粥，辣条');

	select cname,cdesc from category;     
   
	---所有商品
	1.商品ID
	2.商品名称
	3.商品价格
	4.生成日期
	5.商品分类ID
	
	create table product(
		pid int primary key auto_increment,
		pname varchar(10),
		price double,
		pdate timestamp,
		cno int
	);
	
	insert into product values(null,'小米4',998,null,1);
	insert into product values(null,'锤子',2998,null,1);
	insert into product values(null,'耐克',98,null,2);
	insert into product values(null,'茅台',3888,null,3);	
	insert into product values(null,'旺旺雪饼',5,null,4);	
   
	---别名查询
	select p.pname,p.price from product as p;  
  
	select pname as 商品名称,price as 商品价格 from product;
	// 省略as
	select pname 商品名称,price 商品价格 from product;
	
	select distinct price from product;  
	
	---运算查询：仅仅在查询结果上做了运算
	select *,price*1.5 from product;   
	
	select *,price*1.5 as 中间商价格 from product;
	
	---条件查询[where关键字]
	select * from product where price > 60;
	
	<>：不等于，标准SQL语法
	!=：不等于，非标准语法   
   
	select * from product where price <100 or price >900;