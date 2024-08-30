---
layout: post
title: Mysql开发环境
tags: mysql
stickie: true
---

Mysql相关的入门操作，如：windows下安装、启动、停止、删除服务，还有创建用户，修改密码，给用户赋权限等等。
需要注意的是5.0和8.0版本的操作是有区别的，以下主要介绍8.0以上版本的操作。


### windows下安装mysql


+ 下载地址：[https://dev.mysql.com/downloads/mysql/](https://dev.mysql.com/downloads/mysql/)

+ 解压下到以下位置：F:\Program Files\mysql-8.0.26-winx64\bin

+ 启动mysql：
1. 输入命令mysqld --initialize --console来初始化数据库，并记录随机生成的密码：
2. 输入mysqld -install将mysql安装为Windows的服务：
3. 启动mysql服务: net start mysql或sc start mysql
4. 停止MySQL服务：net stop mysqld或sc stop mysqld或sc
5. 删除MySQL服务：sc delete mysqld或mysqld -remove（需先停止服务）
6. 输入mysql -u root -p来登陆数据库，并输入前面记录的临时密码
7. 登陆成功后输入命令ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '********';
8. FLUSH PRIVILEGES; 
9. 并输入commit;提交：



### 创建用户
```mysql
create user 'alpha'@'%' IDENTIFIED WITH mysql_native_password BY '********';
create database alpha;
grant all privileges on alpha.* to 'alpha'@'%';
flush privileges; 
```

### MySQL备份与恢复

```shell
# 备份数据库
mysqldump -udbuser -pdbpassword dbname > dbname.sql

# 恢复数据库
mysql -udbuser -pdbpassword dbname < dbname.sql

```