# RedisCache

参照[Scaling Memcache at Facebook](https://www.usenix.org/system/files/conference/nsdi13/nsdi13-final170_update.pdf)在redis上重放了FB的工作，具体包含以下内容：

* 租约机制，防止数据一致性
* 数据版本查询，客户端允许通过版本进行查询

# env

 * redis-6.2.3
