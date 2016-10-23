---
title: JDK安装指南
date: 2016-06-17 10:40:20
tags: 
  - JDK
  - 软件  
categories: 
  - 技术
---

## 在Windows中配置jdk环境变量步骤

1. 新建**JAVA_HOME**变量，变量值为JDK路径（例如C:\java）；
2. 新建**classpath**变量，变量值为：`.;%JAVA_HOME%\lib;%JAVA_HOME%\lib\tools.jar`；
3. 在path变量（已存在不用新建）添加变量值`%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin`（注意变量值之间用”;”隔开）；
4. 在命令行中执行**javac**命令，如果能正常打印用法说明配置成功。

## 在Linux中配置jdk环境变量步骤

**在.profile或者.bashrc文件中添加如下内容，JAVA_HOME指向jdk路径**

```shell
export JAVA_HOME=/usr/local/java/jdk
export PATH=$JAVA_HOME/bin:$PATH
```