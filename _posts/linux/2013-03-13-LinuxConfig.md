---
layout: post
title:  "linux环境搭建"
date:   2013-03-13
desc: "linux环境搭建"
keywords: "linux,环境"
category: linux
tags: [linux,环境搭建]
icon: icon-html
---

一、文件上传

　　(1).创建文件夹
  	
　　mkdir /itec/upload

　　(2)上传文件
  	
　　apache-tomcat-7.0.68(文件夹)
　　MySQL-5.6.29-1.linux_glibc2.5.i386.rpm-bundle(文件夹)
　　jdk-6u45-linux-i586-rpm.bin(文件)

二、Openjdk卸载
  	
　　rpm -qa|grep java
  	
　　rpm -e –nodeps  ***
  
三、Jdk安装
  	
　　(1)修改权限
  	
　　chmod 755 jdk-6u45-linux-i586-rpm.bin
  	
　　(2)安装jdk
  	
　　./jdk-6u45-linux-i586-rpm.bin
  	rpm –ivh jdk-6u45-linux-i586.rpm
  	
　　(3)修改配置
  	
　　vi /etc/profile
  	
　　export JAVA_HOME=/usr/java/ jdk1.6.0_45
  	
　　export PATH=$PATH:$JAVA_HOME/bin
  	
　　.  /etc/profile
  	
　　.和/之间有空格
  
四、防火墙设置
  	
　　Service iptables stop
  
五、Tomcat安装
  	
　　cd /itec/upload
  	
　　mv apache-tomcat-7.0.68 /itec
  	
　　cd /itec/apache-tomcat-7.0.68/bin
  	
　　./startup.sh
  
六、Mysql安装
  	
　　cd /itec/upload/ MySQL-5.6.29-1.linux_glibc2.5.i386.rpm-bundle
  	
　　(1)安装share
  	
　　rpm –ivh MySQL-shared-5.6.29-1.linux_glibc2.5.i386.rpm
  	
　　(2)安装server
  	
　　rpm –ivh	MySQL-server-5.6.29-1.linux_glibc2.5.i386.rpm
  	
　　rpm -qa|grep mysql
  	
　　rpm -ev --nodeps mysql-libs-5.1.66-2.el6_3.i686
  	
　　(3)安装client
  	
　　rpm –ivh	MySQL-client-5.6.29-1.linux_glibc2.5.i386.rpm
  	
　　(4)修改密码
  	
　　more /root/.mysql_secret
  	service mysql start
  	mysql –uroot –p

  	set password=password('itec_jtwz');
  	
　　(5)修改访问用户权限
  	
　　use mysql
  	
　　select host from user;
  	
　　delete from user where host='localhost';
  	
　　update user set host='%';
  	
　　flush privileges;
  	
　　(6)修改utf8编码
  	
　　show variables like'character%';
  	
　　vi /usr	/my.cnf
  	
　　character-set-server=utf8
  	
　　lower_case_table_names=1;(让linux下mysql大小写不敏感)
  	
　　(7) mysqld_safe --skip-grant-tables
  	
　　 /etc/rc.d/init.d/mysql stop
  	
　　/etc/rc.d/init.d/mysql start
  	
　　sudo mysql -uroot –p
  	
　　(8)删root用户 user
  	
　　Insert root %,localhost
  	
　　INSERT INTO `user` VALUES ('localhost','root','','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','','','','',0,0,0,0);
  	
　　INSERT INTO `user` VALUES ('%','root','','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','','','','',0,0,0,0);

	


	   
	
	

	

	