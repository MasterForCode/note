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
* 9300是Elasticsearch节点间通讯的端口
3. 倒排索引
	通过分词将将关键字和文档进行映射
	

|  序号   | 文档内容    |
| --- | --- |
|  1   |  我是开发人员   |
|    2 |   我是运维人员  |

|  单词ID   |  单词   |  倒排列表   |
| --- | --- | --- |
|  1   |  我   |  1，2   |
|   2  |   开发  |  1   |
|   3  |   运维  |  2   |

