---
title: MySQL编译安装记录
date: 2014-06-19 11:43:25
tags: 
  - MySQL
  - 软件  
categories: 
  - 技术
---

> 记录自己在OpenSUSE中编译安装mysql的过程，实际执行过程中遇到很多或大或小的问题，在谷歌和度娘的帮助下最终都解决了，特将正确的流程记录如下。


### 添加用户组mysql和用户mysql
```shell
$ groupadd mysql
$ useradd -d /home/mysql -m -g mysql mysql
$ passwd mysql
```

### 安装依赖包
```
ncurses-devel bison libaio-devel gcc-c++ （OpenSUSE中使用yast安装）
```

<!-- more -->

### 编译

下载源码包mysql-5.5.34.tar.gz并解压。进入解压后的目录mysql-5.5.34执行如下命令（相关路径可根据实际情况修改）
```shell
$ cmake . -DCMAKE_INSTALL_PREFIX=/home/mysql/mysql -DMYSQL_UNIX_ADDR=/home/mysql/mysql/mysql.sock -DMYSQL_DATADIR=/home/mysql/mysql/data -DDEFAULT_CHARSET=utf8 -DDEFAULT_COLLATION=utf8_general_ci -DWITH_EXTRA_CHARSETS=all -DWITH_MYISAM_STORAGE_ENGINE=1 -DWITH_INNOBASE_STORAGE_ENGINE=1 -DWITH_READLINE=1 -DENABLED_LOCAL_INFILE=1  -DMYSQL_TCP_PORT=3306
$ make
$ make install
```

### 配置MySQL

```shell
$ chown -R mysql.mysql /home/mysql/mysql
$ /home/mysql/mysql/scripts/mysql_install_db –user=mysql –basedir=/home/mysql/mysql –datadir=/home/mysql/mysql/data
$ cd /home/mysql/mysql/support-files
$ cp mysql.server /etc/init.d/mysql
$ cp my-medium.cnf /etc/my.cnf
```

### 添加mysql开机启动

```shell
$ chkconfig -add mysql
$ chkconfig mysql on
#启动mysql
$ service mysql start
#修改root用户密码
$ /home/mysql/mysql/bin/mysqladmin -u root password '123456'
```

### 登陆mysql后创建用户并赋予权限
```shell
mysql> GRANT ALL PRIVILEGES ON *.* TO root@"%" IDENTIFIED BY '123456' WITH GRANT OPTION;
```