---
layout: post
title: sqlite3加密
tags: sqlite3
stickie: true
---

sqlite3是轻量级,程序员常用的数据库,由于标准的sqlite3数据库是不带有密码功能的,任何人都能浏览数据库内的文件,因此,在某些场景下需要对sqlite数据库进行加密,例如微信的数据库就使用了
sqlite加密技术.

### 加密sqlite数据库的软件
* sqleet
* SQLite3MultipleCiphers
* SQLCipher
* ...

以下sqleet为例

### 需要安装sqleet
下载安装包:[https://gitee.com/mirrors/sqleet](https://gitee.com/mirrors/sqleet)

### 编译 sqleet:
```shell
# UNIX
gcc sqleet.c shell.c -o sqleet -lpthread -ldl

# Windows
gcc sqleet.c shell.c -o sqleet

```


### 编译sqlite3
```shell
# UNIX
gcc -shared -Wall  -fPIC sqleet.c -lc -lpthread -ldl -o libsqlite3.so

# Windows
gcc -shared -Wall  -fPIC sqleet.c -lpthread -o sqlite3.dll
```

### 使用sqlite3

使用时需要`LD_PRELOAD`去加载

```shell
LD_PRELOAD=$(pwd)/lib/libsqlite3.so python xxx
```