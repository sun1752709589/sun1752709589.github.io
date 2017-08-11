---
layout: post
title: elasticsearch个人使用心得
---

elasticsearch个人使用心得笔记

### 修改某一索引副本数
```
curl -XPUT 'localhost:9200/<index_name>/_settings' -d '{"number_of_replicas": 0}'
可以将一些不重要而且比较老的数据设置副本数为0以节省磁盘空间
```
### 某一索引为yellow原因及修复方法
```
https://www.datadoghq.com/blog/elasticsearch-unassigned-shards/
```