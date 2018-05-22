<center>  

# javaEE框架师之路  

<hr width = "50%">  

## 三、MySQL02（Structured Query Language）    

</center>    
  
### 多表之间的关系如何来维护

外键约束: foreign key

  - 给product中的这个cno 添加一个外键约束

    alter table product add foreign key(cno)  references  category(cid);   
   
  - 从分类表中,删除分类为5信息,

    - delete from category where cid =5;  //删除失败
    - 首先得去product表, 删除所有分类ID5  商品   

### 建数据库原则:

  - 通常情况下,一个项目/应用建一个数据库

### 多表之间的建表原则

  * 一对多 : 商品和分类

    - 建表原则: 在多的一方添加一个外键,指向一的一方的主键  ​

  - 多对多: 老师和学生, 学生和课程

    建表原则: 建立一张中间表,将多对多的关系,拆分成一对多的关系,中间表至少要有两个外键,分别指向原来的那两张表  
   
  - 一对一: 班级和班长, 公民和身份证, 国家和国旗

    - 建表原则:  

      - 将一对一的情况,当作是一对多情况处理,在任意一张表添加一个外键,并且这个外键要唯一,指向另外一张表
      - 直接将两张表合并成一张表
      - 将两张表的主键建立起连接,让两张表里面主键相等

    - 实际用途: 用的不是很多.    (拆表操作  )

      - 相亲网站: 
        - 个人信息 : 姓名,性别,年龄,身高,体重,三围,兴趣爱好,(年收入,  特长,学历, 职业, 择偶目标,要求)
        - 拆表操作 : 将个人的常用信息和不常用信息,减少表的臃肿, 
   
---  

### 网上商城表实例的分析: 用户购物流程  
   

* 用户表 (用户的ID,用户名,密码,手机)
  
		create table user(  
		  uid int primary key auto_increment,  
		    username varchar(31),  
		    password varchar(31),  
		    phone  varchar(11)  
		);    
   
		insert into user values(1,'zhangsan','123','13811118888');   
   
* 订单表 (订单编号,总价,订单时间 ,地址,外键用户的ID)

		create table orders(
			oid int primary key auto_increment,
			sum int not null,
			otime timestamp,
			address varchar(100),
			uno int,
			foreign key(uno) references user(uid)
		);
		    
		insert into orders values(1,200,null,'黑马前台旁边小黑屋',1);
		insert into orders values(2,250,null,'黑马后台旁边1702',1);   
    
* 商品表 (商品ID, 商品名称,商品价格,外键cno)

	    create table product(
	    	pid int primary key auto_increment,
	      	pname varchar(10),
	      	price double,
	      	cno int,
	      	foreign key(cno) references category(cid)
	    );
	
	    insert into product values(null,'小米mix4',998,1);
	    insert into product values(null,'锤子',2888,1);
	    insert into product values(null,'阿迪王',99,2);
	    insert into product values(null,'老村长',88,3);
	    insert into product values(null,'劲酒',35,3);
	    insert into product values(null,'小熊饼干',1,4);
	    insert into product values(null,'卫龙辣条',1,5);
	    insert into product values(null,'旺旺大饼',1,5);     
  
* 订单项: 中间表(订单ID,商品ID,商品数量,订单项总价)

		create table orderitem(
			ono int,
		  	pno int,
		  	foreign key(ono) references orders(oid),
		  	foreign key(pno) references product(pid),
		  	ocount int,
		  	subsum double
		);
		--给1号订单添加商品 200块钱的商品
		insert into orderitem values(1,7,100,100);
		insert into orderitem values(1,8,101,100);
		
		--给2号订单添加商品 250块钱的商品 ()
		insert into orderitem values(2,5,1,35);
		insert into orderitem values(2,3,3,99);    
 
   
* 商品分类表(分类ID,分类名称,分类描述)

	    create table category(
	    	cid int primary key auto_increment,
	      	cname varchar(15),
	      	cdesc varchar(100)
	    );
	
	    insert into category values(null,'手机数码','电子产品,黑马生产');
	    insert into category values(null,'鞋靴箱包','江南皮鞋厂倾情打造');
	    insert into category values(null,'香烟酒水','黄鹤楼,茅台,二锅头');
	    insert into category values(null,'酸奶饼干','娃哈哈,蒙牛酸酸乳');
	    insert into category values(null,'馋嘴零食','瓜子花生,八宝粥,辣条');     
   
---
    
#### 多表之间的关系如何维护: 
外键约束 :   foreign key    

* 添加一个外键: 
	- alter table product add foreign key(cno)  references category(cid);
	- foreign key(cno) references category(cid)
	- 删除的时候, 先删除外键关联的所有数据,再才能删除分类的数据  
   
#### 建表原则:
  - 一对多:
    - 建表原则: 在多的一方增加一个外键,指向一的一方
  - 多对多:
    - 建表原则: 将多对多转成一对多的关系,创建一张中间表
	    - 拆成一对多
	    - 创建一张中间表, 至少要有两个外键, 指向原来的表
  - 一对一: 不常用, 拆表操作
    - 建表原则:  将两张表合并成一张表
      - 将两张表的主键建立起关系
      - 将一对一的关系当作一对多的关系去处理


#### 主键约束: 默认就是不能为空, 唯一

-  外键都是指向另外一张表的主键
-  主键一张表只能有一个

#### 唯一约束: 列的内容, 必须是唯一, 不能出现重复情况, 为空

- 唯一约束不可以作为其它表的外键
- 可以有多个唯一约束
   
#### 多表查询

- 交叉连接查询：笛卡尔积
  
		select * from product,category where cno=cid;
		select * from product as p,category as c where p.cno=c.cid;
		select * from product p,category c where p.cno=c.cid;

- 内连接查询
     
		//隐式内连接:在查询结果上进行调节过滤
		select * from product p,category c where p.cno=c.cid;
		//显示内连接:带着条件去查询,执行效率高
		select * from product p inner join category c on p.cno=c.cid;

- 左外连接  

		//会将左表中的数据全部显示，右表没有对应数据，用null代替
		select * from product p left outer join category c on p.cno=c.cid;

- 右外连接    

		select * from product p right outer join category c on p.cno=c.cid;   
    
#### 分页查询

- 每页数据数据3
- 起始索引从0 
- 第1页: 0
- 第2页: 3

  起始索引:  index 代表显示第几页 页数从1开始，每页显示3条数据

  	startIndex  = (index-1)*3
   
第一个参数是索引，第二个参数显示的个数

	select * from product limit 0,3;
	
	select * from product limit 3,3;    
    
#### 子查询(非常重要)

查询出(商品名称,商品分类名称)信息
  
	//左连接
	select p.pname,c.cname from product p left outer join category c on p.cno=c.cid;

	//子查询
	select pname,(select cname from category c where p.cno=c.cid) as 商品分类名称 from product;

查询分类名称为手机数码的所有商品
   
	//1.查询分类名为手机数码的ID
	select cid from category where cname ='手机数码';
	//2.得出ID为手机数码的结果
	select * from product where cno=(select cid from category where cname ='手机数码');
  
---   
  
### 多表查询练习数据

#### 员工信息表

	CREATE TABLE emp(
		empno INT,
		ename VARCHAR(50),
		job VARCHAR(50),
		mgr	INT,
		hiredate DATE,
		sal	DECIMAL(7,2),
		comm DECIMAL(7,2),
		deptno INT
	) ;

	INSERT INTO emp values(7369,'SMITH','CLERK',7902,'1980-12-17',800,NULL,20);
	INSERT INTO emp values(7499,'ALLEN','SALESMAN',7698,'1981-02-20',1600,300,30);
	INSERT INTO emp values(7521,'WARD','SALESMAN',7698,'1981-02-22',1250,500,30);
	INSERT INTO emp values(7566,'JONES','MANAGER',7839,'1981-04-02',2975,NULL,20);
	INSERT INTO emp values(7654,'MARTIN','SALESMAN',7698,'1981-09-28',1250,1400,30);
	INSERT INTO emp values(7698,'BLAKE','MANAGER',7839,'1981-05-01',2850,NULL,30);
	INSERT INTO emp values(7782,'CLARK','MANAGER',7839,'1981-06-09',2450,NULL,10);
	INSERT INTO emp values(7788,'SCOTT','ANALYST',7566,'1987-04-19',3000,NULL,20);
	INSERT INTO emp values(7839,'KING','PRESIDENT',NULL,'1981-11-17',5000,NULL,10);
	INSERT INTO emp values(7844,'TURNER','SALESMAN',7698,'1981-09-08',1500,0,30);
	INSERT INTO emp values(7876,'ADAMS','CLERK',7788,'1987-05-23',1100,NULL,20);
	INSERT INTO emp values(7900,'JAMES','CLERK',7698,'1981-12-03',950,NULL,30);
	INSERT INTO emp values(7902,'FORD','ANALYST',7566,'1981-12-03',3000,NULL,20);
	INSERT INTO emp values(7934,'MILLER','CLERK',7782,'1982-01-23',1300,NULL,10);
	INSERT INTO emp values(7981,'MILLER','CLERK',7788,'1992-01-23',2600,500,20);


#### 部门信息表


	CREATE TABLE dept(
		deptno		INT,
		dname		varchar(14),
		loc			varchar(13)
	);
	
	INSERT INTO dept values(10, 'ACCOUNTING', 'NEW YORK');
	INSERT INTO dept values(20, 'RESEARCH', 'DALLAS');
	INSERT INTO dept values(30, 'SALES', 'CHICAGO');
	INSERT INTO dept values(40, 'OPERATIONS', 'BOSTON');    

## 查询实例   
  
	//最高工资
	select max(sal) from emp;
	//最少工资
	select min(sal) from emp;
	//最高工资的员工信息
	select * from emp where sal = (select max(sal) from emp);
	//查询出高于10号部门的平均工资的员工信息
	1、找出10号部门的平均工资
	select avg(sal) from emp where deptno=10;
	2、高于结果的员工信息
	select * from emp where sal>(select avg(sal) from emp where deptno=10);  
	  
	//找出任意一个比10号部门员工工资高的员工
	select sal from emp where detptno = 10;
	
	select * from emp where sal > any(select sal from emp where detptno) and detptno != 10;    
    
	//和10号部门同名同工作的员工信息
	1.查询出10号部门所有人 名字和工作
	select ename,job from emp where deptno=10;
	2.select * from emp where (ename,job) in (select ename,job from emp where deptno=10) and deptno !=10;
	  
	//select后面接子查询
	//获取员工的名字和部门的名字
	select ename，deptno from emp;
	select ename,(select dname from dept d where d.deptno=e.deptno) 部门名字 from emp e;
	   
