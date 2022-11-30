---
layout: post
title: Mysql相关
tags: mysql
---


### windows下安装mysql


+ 下载地址：[https://dev.mysql.com/downloads/mysql/](https://dev.mysql.com/downloads/mysql/)

+ 解压下到以下位置：F:\Program Files\mysql-8.0.26-winx64\bin

+ 启动mysql：

    * 输入命令mysqld --initialize --console来初始化数据库，并记录随机生成的密码：
    * 输入mysqld -install将mysql安装为Windows的服务：
    * 启动mysql服务: net start mysql或sc start mysql
    * 停止MySQL服务：net stop mysqld或sc stop mysqld或sc
    * 删除MySQL服务：sc delete mysqld或mysqld -remove（需先停止服务）
    * 输入mysql -u root -p来登陆数据库，并输入前面记录的临时密码
    * 登陆成功后输入命令ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '********';
    * FLUSH PRIVILEGES; 
    * 并输入commit;提交：



### 创建用户
```mysql
create user 'alpha'@'%' IDENTIFIED WITH mysql_native_password BY '********';
create database alpha;
grant all privileges on alpha.* to 'alpha'@'%';
flush privileges; 
```

