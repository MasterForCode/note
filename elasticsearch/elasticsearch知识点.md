---
title: elasticsearch
tags: elasticesearch
time: 2019.1.6
---
1. 存储结构
* Elasticsearch是文件存储，是面向文档型数据库，一条数据在这里就是一个文档，用JSON作为文档序列化格式
* 类比数据库索引（index对应数据库）=》类型（type对应表）=》文档（document对应行）=》字段（fields对应列）
2. 9200端口和9300端口
* 9200是Elasticsearch为restful查询提供的端口
* 9300是Elasticsearch节点间通讯或者客户端可服务端通讯的端口
