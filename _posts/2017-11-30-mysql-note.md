---
layout: post
title: MySQL使用总结
---

MySQL使用总结

### MySQL授权grant
```
mysql授权
grant all privileges on *.* to 'linkface'@'%' identified by 'linkface';
flush privileges;
```
### 修改sql_mode的语法
```
SET GLOBAL sql_mode = '';
SET SESSION sql_mode = '';
```
