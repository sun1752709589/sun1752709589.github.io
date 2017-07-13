---
layout: post
title: 如何加速rspec测试速度
---

### 加速rspec测试速度

```
偶然发现的gem包:https://github.com/grosser/parallel_tests
原理:计算机多核开多个测试进程,并且进程之间用用不同数据库,防止干扰.
用法:具体用法文档都有,我就不写了
结论:幻腾主服务测试时间从原先的30min掉到了20min,提速1/3;
    由于jenkins构建时间=测试 + 部署,所以实际提速测试时间为:1/3 < it < 1/2
    受限于jenkins服务器核数,现在只能提速这么多,理论上可以缩短测试时间到1/n
```