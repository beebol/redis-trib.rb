redis-trib.rb是redis官方推出的管理redis集群的工具，集成在redis的源码src目录下，是基于redis提供的集群命令封装成简单、便捷、实用的操作工具。redis-trib.rb是redis作者用ruby完成的。
其中一个rebalance，使用非常多，在扩容节点后需要进行均衡slot的自动均衡，做slot迁移。但由于这个功能在3.0.6的版本中才有，为什么这个版本才有的原因，可能是之前不支持mutil migrate的原因。

如果需要在3.0.6以前的版本，或者redis集群中存在3.0.6以前的版本，那和就无法使用这个工具的rebalance工具，比较遗憾。但不不要紧，这里这这个脚本是可以进行rebalance的，只不过速度没有在3.0.6以及以上版本那么快。

3.0.6以前版本使用工具报如下错误：
···
redis-trib.rb rebalance --threshold 1 --use-empty-masters 127.0.0.1:9001 
>>> Performing Cluster Check (using node 127.0.0.1:9001)
[OK] All nodes agree about slots configuration.
>>> Check for open slots...
>>> Check slots coverage...
[OK] All 16384 slots covered.
>>> Rebalancing across 5 nodes. Total weight = 5
Moving 820 slots from 127.0.0.1:9003 to 127.0.0.1:9005

[ERR] ERR syntax error
···

下载使用后不会报这个问题了。


使用，下载后在可以运行的redis-trib.rb机器上直接可执行。
