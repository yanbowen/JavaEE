## 安装java，Tomcat，MySQL
  
在Linux命令行输入vim时提示：-bash:vim :common not found
  
	输入 rpm -qa|grep vim 命令,查看返回结果，如果返回的是三条结果：
	
	vim-minimal-7.0.109-6.el5
	vim-common-7.0.109-7.2.el5
	vim-enhanced-7.0.109-7.2.el5
	
	则说明vim已经正确安装，如果缺少一条，则需要单独安装  
  
全部重新安装：

	如果上面的三条都沒有返回, 可以直接用 yum -y install vim* 命令
	yum -y install vim*   
   
配置环境变量：  
  
	1. vim /etc/profile  
	
	2. 在末尾行添加
	#set java environment
	JAVA_HOME=/usr/local/src/java/jdk1.7.0_71
	CLASSPATH=.:$JAVA_HOME/lib.tools.jar
	PATH=$JAVA_HOME/bin:$PATH
	export JAVA_HOME CLASSPATH PATH
	保存退出   
	   
	3. source /etc/profile  使更改的配置立即生效  
	
	4. java -version  查看JDK版本信息，如果显示出1.7.0证明成功   

  
Centos 7 开放查看端口 防火墙关闭打开   

	查看已经开放的端口：
	firewall-cmd --list-ports
	  
	开启端口  
	firewall-cmd --zone=public --add-port=80/tcp --permanent
	  

	命令含义：
	–zone #作用域
	–add-port=80/tcp #添加端口，格式为：端口/通讯协议
	–permanent #永久生效，没有此参数重启后失效   
	    

	重启防火墙   
	firewall-cmd --reload #重启firewall
	systemctl stop firewalld.service #停止firewall
	systemctl disable firewalld.service #禁止firewall开机启动   
    
  
	查询端口号80 是否开启：
	firewall-cmd --query-port=80/tcp
  
	永久开放80端口号：
	firewall-cmd --permanent --zone=public --add-port=80/tcp

	移除80端口号：
	firewall-cmd --permanent --zone=public --remove-port=80/tcp   
   
出现以上安装错误列表的原因是：系统已经安装了其他版本的mysql-libs包和mysql数据库文件导致不兼容。  
  
	yum remove mysql-libs  
  
	监测MySQL是否启动
	systemctl status mysqld.service
	启动MySQL
	systemctl start  mysqld.service
	
	rpm -qa | grep mysql
   
登录MySQL，设置远程访问权限  
  
	grant all privileges on *.* to 'root' @'%' identified by '123456'; 
	flush privileges;  
   
	永久开放3306端口号：
	firewall-cmd --permanent --zone=public --add-port=3306/tcp  
   
