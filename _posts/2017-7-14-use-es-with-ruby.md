---
layout: post
title: ruby中使用elasticsearch
---

文章介绍了ruby中使用searchkick作为elasticsearch客户端

### ruby遇上elasticsearch
```
客户端:https://github.com/ankane/searchkick
sql客户端:https://github.com/NLPchina/elasticsearch-sql

class Elas < ActiveRecord::Base
  searchkick index_name: :index_name

  def index_name
     return self.galaxy_name
  end
end

search_hash = {'@timestamp' => {gte: DateTime.parse(@start_time) - 8.hours, lte: DateTime.parse(@end_time) - 8.hours}}
search_hash.merge!({remote_ip: @ip}) if @ip && @ip.size >= 7
search_hash.merge!({request: @keywork}) if @keywork && @keywork.size > 0
@logs = Elas.search("*", where: search_hash, index_name: 'nginx_*', load: false, order: {'@timestamp' => 'desc'}, limit: 999)
```