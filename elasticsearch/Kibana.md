---
title: Kibana
tags: Kibana
grammar_cjkRuby: true
---


1. 安装
* 下载解压
  ```bash
  # 下载
  [root@localhost ~]# wget https://www.elastic.co/downloads/kibana
  # 解压
  [root@localhost ~]# tar -zxvf kibana-6.5.3-linux-x86_64.tar.gz -C /usr/local/
  ````
* 修改配置文件
  ```bash
  [root@localhost ~]# vi /usr/local/kibana-6.5.3-linux-x86_64/config/kibana.yml 
  # 添加
  server.host: "192.168..0.111"
  elasticsearch.url: "http://192.168.0.111:9200"
  ```
* 验证
  ```bash
  # 开放端口
  [root@localhost ~]# firewall-cmd --zone=public --add-port=5601/tcp --permanent
  [root@localhost ~]# firewall-cmd --reload
  # 启动
  [root@localhost ~]# /usr/local/kibana-6.5.3-linux-x86_64/bin/kibana
  ```
* [访问](http://192.168.0.111:5601)
2. 操作Elasticsearch
* 操作索引
  ```bash
  # 创建索引
  PUT /myindex
  # 删除索引
  DELETE /myindex
  # 查询索引
  GET /myindex
  ```
 * 文档操作
   ```bash
   # 创建文档，格式为/索引/类型/id（PUT方式）
   PUT /myindex/user/1
   {
   "name": "张三",
   "age": 13
   }
   # 创建文档，格式为/索引/类型（POST方式）
   # 自动生成id
   POST /myindex/user/1
   {
   "name": "张三",
   "age": 13
   }  
   # 查询文档
   GET /myindex/user/1
   # user类型下的所有文档
   GET /myindex/user/_search
   # 根据多个id查询
   GET /myindex/user/_mget
   {
	"ids": [1, 2]
   }
   # 条件查询
   GET /myindex/user/_search?q=age:13
   # TO要大写
   GET /myindex/user/_search?q=age[10 TO 15]
   # 查询并排序
   GET /myindex/user/_search?q=age[10 TO 15]&sort=age:desc
   #指定查询结果集数据量（分页）
   GET /myindex/user/_search?q=age[10 TO 15]&sort=age:desc&from=0&size=2
   ```