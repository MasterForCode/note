---
title: Elasticsearch安装
tags: elasticsearch
grammar_cjkRuby: true
---

# 环境
1. 安装Java环境
*  [下载jdk1.8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html  )压缩文件  
*  解压
	``` bash
	# 创建文件
	[root@localhost ~]# mkdir /usr/local/java
	# 解压
	[root@localhost ~]# tar -zxvf filename -C /usr/local/java
	```
*  编辑/etc/下的profile文件，配置环境变量
	``` bash
	[root@localhost software]# vim /etc/profile
	# jdk1.8.0_101根据具体的小版本修改
	export JAVA_HOME=/usr/local/java/jdk1.8.0_101
	export JRE_HOME=${JAVA_HOME}/jre
	export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
	export PATH=${JAVA_HOME}/bin:$PATH
	```
* 使/etc/profile生效
	``` bash
	[root@localhost jdk1.8.0_101]# source /etc/profile
	```
	* 测试
	``` bash
	[root@localhost jdk1.8.0_101]# java -version
	java version "1.8.0_101"
	Java(TM) SE Runtime Environment (build 1.8.0_101-b13)
	Java HotSpot(TM) 64-Bit Server VM (build 25.101-b13, mixed mode)
	```
# 安装
2. 安装Elasticsearch
* 下载Elasticsearch
 ```bash
 # 将版本替换成最新版本
[root@localhost ~]# wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-6.5.3.tar.gz
 ```
 * 解压到指定目录
  ```bash
  [root@localhost ~]# tar -zxvf elasticsearch-6.5.3.tar.gz -C /usr/local/
  ```
* 默认占用1g内存，可已修改成512m
* 9200端口是节点与外部通讯使用
* 9300端口是集群时节点间通讯使用