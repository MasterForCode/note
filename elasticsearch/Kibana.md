---
title: Kibana
tags: Kibana
grammar_cjkRuby: true
---


1. 安装
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
 # 创建文档，格式为/索引/类型/id
 PUT /myindex/user/1
 {
 	"name": "张三",
	"age": 12
	}
	# 查询文档
	GET /myindex
 ```