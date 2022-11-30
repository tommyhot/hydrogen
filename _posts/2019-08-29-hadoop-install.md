---
layout: post
title: Hadoop-2.7.2安装教程!
tags: 大数据 hadoop
---


主要参考:
[Hadoop2.7.2之集群搭建（高可用）](http://blog.csdn.net/uq_jin/article/details/51513307)、[Hadoop2.7.2之集群搭建（三台）](http://blog.csdn.net/uq_jin/article/details/51487439)

### 1、安装JDK
### 2、配置免密登录
确认系统已经安装了SSH
~~~sh
rpm –qa | grep openssh
rpm –qa | grep rsync
yum install ssh -->安装SSH协议
yum install rsync -->rsync是一个远程数据同步工具，可通过LAN/WAN快速同步多台
service sshd restart -->启动服务
~~~
生成秘钥对
~~~sh
ssh-keygen –t rsa –P '' 
-->直接回车生成的密钥对：id_rsa和id_rsa.pub，默认存储在"/root/.ssh"目录下
~~~
把id_rsa.pub追加到授权的key里面去
~~~sh
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
~~~
修改授权key的权限
~~~sh
chmod 600 ~/.ssh/authorized_keys
~~~
待参考方法
~~~sh
ssh-copy-id master
ssh-copy-id slave1
ssh-copy-id slave2
~~~

### 3、配置环境变量
~~~sh
# vi ~/.bashrc
#export HIVE_HOME=/usr/local/hive
#export PATH=$HIVE_HOME/bin:$PATH
#export SCALA_HOME=/usr/lib/scala/scala-2.10.5
export JAVA_HOME=/usr/java/jdk1.8.0_91
export HADOOP_HOME=/usr/local/hadoop/hadoop-2.7.2
#export SPARK_HOME=/usr/local/spark/spark-2.0.0
#export SPARK_HOME=/usr/local/spark/spark-1.5.1
export JRE_HOME=${JAVA_HOME}/jre
export CLASS_PATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=:${JAVA_HOME}/bin:${SCALA_HOME}/bin:${HADOOP_HOME}/bin:${SPARK_HOME}/bin:$PATH
#export JAVA_OPTS="$JAVA_OPTS -Dhttp.proxyHost=proxy -Dhttp.proxyPort=port -Dhttps.proxyHost=proxy -Dhttps.proxyPort=port"
export LD_LIBRARY_PATH=$HADOOP_HOME/lib/native
~~~
`配置环境变量时，可以考虑将不同版本hadoop建立软连接`

### 替换系统的yum，安装163.com源

参考:[RedHat Enterprise Linux 6.4使用Centos 6 的yum源](http://blog.sina.com.cn/s/blog_50f908410101cto6.html)
### 安装gcc,gcc+c++

### 复制虚拟机后，重新配置网卡
# 删除eth1网卡
* 编辑/etc/udev/rules.d/70-persistent-net.rules文件
* 把NAME="eth0"的那行配置注释掉或者删掉，把NAME="eth1"的修改成NAME="eth0"
* 更改网卡配置文件，/etc/sysconfig/network-scripts/ifcfg-eth0
* 将HWADDR的值修改为/etc/udev/rules.d/70-persistent-net.rules文件中的新值
* 修改/etc/sysconfig/network，更改主机名
* reboot
* 启用eth0 ifconfig eth0 up 


参考:[VMware虚拟机克隆Linux系统后找不到eth0网卡的问题](http://www.linuxidc.com/Linux/2013-01/78427.htm)


如果出现问题，可尝试进入DEBUG模式
~~~
export HADOOP_ROOT_LOGGER=DEBUG,console
~~~

无法加载hadoop库的时候有可能是glibc库的版本过低
下载[glibc-2.14.1.tar.gz](http://ftp.ntu.edu.tw/gnu/glibc/glibc-2.14.1.tar.gz) 放入 /data文件夹下，解压出glibc-2.14.1
~~~
先进入非源目录文件夹 
mkdir /usr/local/glibc
cd /usr/local/glibc
/data/glibc-2.14.1/configure  --prefix=/usr --disable-profile --enable-add-ons --with-headers=/usr/include --with-binutils=/usr/bin
make
~~~
编译glic需要gcc,gcc+c++编译器，采用yum install 安装，
RedHat发行版无法进行yum安装，故需要删除原有的yum，安装163.com的yum 源

这里要注意，更新系统里的链接（我的是/lib64/libc.so.6) 很容易出错，我不清楚有没有更好的办法，一般都是删除旧链接，建立新链接暂时不make install，但删除旧链接后，很多命令直接不能用了，因为此时中不到glibc的库了。这个时候就需要临时指定一个glibc库，方法如下：
~~~
cp libc.so /lib64/libc-2.14.so
rm -rf /lib64/libc.so.6
LD_PRELOAD=/lib64/libc-2.14.so ln -s /lib64/libc-2.14.so /lib64/libc.so.6
~~~


### 查看和进程
	ps -ef|grep spark-shell


###
	export HADOOP_ROOT_LOGGER=INFO,console