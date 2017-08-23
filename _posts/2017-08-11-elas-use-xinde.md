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
### 开关索引
```
curl -XPOST 'localhost:9200/<index_name>/_close'
curl -XPOST 'localhost:9200/<index_name>/_open'
```
### 某一索引为yellow原因及修复方法
```
https://www.datadoghq.com/blog/elasticsearch-unassigned-shards/
1)查看某一副本分片未分配的原因
  curl -XGET localhost:9200/_cat/shards?h=index,shard,prirep,state,unassigned.reason| grep UNASSIGNED
2)删除索引
  curl -XDELETE 'localhost:9200/index_name/'
3)能够用单个命令来删除所有数据可能会导致可怕的后果。如果你想要避免意外的大量删除, 你可以在你的 elasticsearch.yml 做如下配置：
  action.destructive_requires_name: true
4)查看节点磁盘占用比例
  curl -s 'localhost:9200/_cat/allocation?v'
  结果如:
  shards disk.indices disk.used disk.avail disk.total disk.percent host         ip           node
   508      159.9gb   192.8gb    397.4gb    590.3gb           32 x.x.x.x      x.x.x.x        elas1
   509      158.8gb   213.1gb    475.5gb    688.7gb           30 x.x.x.x      x.x.x.x        elas2
5)设置当磁盘占用率达到多少时不再分配分片
  curl -XPUT 'localhost:9200/_cluster/settings' -d
  '{
      "transient": {
        "cluster.routing.allocation.disk.watermark.low": "90%"
      }
  }'
```
### x-pack相关
```
1)Change the passwords of the built in kibana, logstash_system and elastic users:
  curl -XPUT -u elastic 'localhost:9200/_xpack/security/user/elastic/_password' -H "Content-Type: application/json" -d '{
  "password" : "elasticpassword"
  }'

  curl -XPUT -u elastic 'localhost:9200/_xpack/security/user/kibana/_password' -H "Content-Type: application/json" -d '{
  "password" : "kibanapassword"
  }'

  curl -XPUT -u elastic 'localhost:9200/_xpack/security/user/logstash_system/_password' -H "Content-Type: application/json" -d '{
  "password" : "logstashpassword"
  }'
```