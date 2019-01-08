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
  [root@localhost ~]# wget  https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-6.5.3.tar.gz
  ```
* 解压到指定目录
  ```bash
  [root@localhost ~]# tar -zxvf elasticsearch-6.5.3.tar.gz -C /usr/local/
  ```
* 修改配置文件
  ```bash
  [root@localhost ~]# vi /usr/local/elasticsearch-6.5.3/config/elasticsearch.yml
  # 添加如下内容
  cluster.name: myes
  network.host: 192.168.0.111
  http.port: 9200
  ```
* 创建使用es的用户及用户组
  ```bash
  # 创建用户组
  [root@localhost ~]# groupadd es
  # 创建用户
  [root@localhost ~]# useradd es -g es -p wangbin_123
  # 分配权限
  [root@localhost ~]# chown -R es:es /usr/local/elasticsearch-6.5.3/
  ```
* 修改系统参数
  ```bash
  [root@localhost ~]# vi /etc/security/limits.conf
  # 最后添加
  es hard nofile 65536
  es soft nofile 65536
  [root@localhost ~]#  vi /etc/sysctl.conf
  # 最后添加
  vm.max_map_count=262144
  ```
* 开放端口
  ```bash
  # 开放需要的端口
  [root@localhost ~]# firewall-cmd --zone=public --add-port=9200/tcp --permanent
  [root@localhost ~]# firewall-cmd --zone=public --add-port=9300/tcp --permanent
  [root@localhost ~]# firewall-cmd --reload
  ```
  
* 运行Elasticsearch
  ```bash
  # 切换用户
  [root@localhost ~]# su - es
  [root@localhost ~]# /usr/local/elasticsearch-6.5.3/bin/elasticsearch
  ```
* [访问](http://192.168.0.111:9200/)

3. 安装ik分词器
* 下载与Elasticsearch版本相同的[分词器](https://github.com/medcl/elasticsearch-analysis-ik/releases)
* 上传到服务器并解压到Elasticsearch的安装目录下的plugins
  ```bash
  # 先终止Elasticsearch
  # 解压到指定目录
  [es@localhost ~]# unzip elasticsearch-analysis-ik-6.5.3.zip -d /usr/local/elasticsearch-6.5.3/plugins/elasticsearch-analysis-ik-6.5.3
  # 切换到Elasticsearch用户
  [es@localhost ~]# su - es
  # 启动
  [es@localhost ~]$ /usr/local/elasticsearch-6.5.3/bin/elasticsearch
  ```
  
 4. 自定义分词器的扩展字典
    ```bash
    # 新增文件并写入自定义字典  
	[es@localhost ~]$ vi /usr/local/elasticsearch-6.5.3/plugins/elasticsearch-analysis-ik-6.5.3/config/new_word.dic                      
	[es@localhost ~]$ vi /usr/local/elasticsearch-6.5.3/plugins/elasticsearch-analysis-ik-6.5.3/config/IKAnalyzer.cfg.xml 
	修改成
	extra_main.dic                  extra_single_word_low_freq.dic  main.dic                        quantifier.dic                  surname.dic
	extra_single_word.dic           extra_stopword.dic              new_word.dic                    stopword.dic                    
	extra_single_word_full.dic      IKAnalyzer.cfg.xml              preposition.dic                 suffix.dic                      
	[es@localhost ~]$ vi /usr/local/elasticsearch-6.5.3/plugins/elasticsearch-analysis-ik-6.5.3/config/IKAnalyzer.cfg.xml 
	<?xml version="1.0" encoding="UTF-8"?>
	<!DOCTYPE properties SYSTEM "http://java.sun.com/dtd/properties.dtd">
	<properties>
			<comment>IK Analyzer 扩展配置</comment>
			<!--用户可以在这里配置自己的扩展字典 -->
			<entry key="ext_dict">new_word.dic</entry>
			 <!--用户可以在这里配置自己的扩展停止词字典-->
			<entry key="ext_stopwords"></entry>
			<!--用户可以在这里配置远程扩展字典 -->
			<!-- <entry key="remote_ext_dict">words_location</entry> -->
			<!--用户可以在这里配置远程扩展停止词字典-->
			<!-- <entry key="remote_ext_stopwords">words_location</entry> -->
	</properties>
	# 启动Elasticsearch
	[es@localhost ~]$ /usr/local/elasticsearch-6.5.3/bin/elasticsearch
   ```