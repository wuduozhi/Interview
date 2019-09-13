# 分布式基础知识

## 分布式锁

* [架构师带你玩转分布式锁 ](https://mp.weixin.qq.com/s?__biz=MzI4NDY5Mjc1Mg==&mid=2247486313&idx=1&sn=9b097bf3ce2d13e0afc3ed1e6b0df674&chksm=ebf6d316dc815a006232abdfe700cdedeb417ec9ffe9e1ea67b255f9bb8c58236af1f314c5f8&scene=27#wechat_redirect)
* [别吵吵，分布式锁也是锁](https://mp.weixin.qq.com/s?__biz=MzAxOTc0NzExNg==&mid=2665515354&idx=1&sn=769cb0b8f0bd54c8b721931880d3e077&chksm=80d67119b7a1f80f3504cb7f9c6808b2113f681572cd59a0ce0b93f464bbec009fd5dae85fa6&scene=27#wechat_redirect)

分布式锁三种实现方式：

* 基于数据库实现
    * 乐观锁 （CAS）
    * 悲观锁 （for update）
* 基于 Redis 实现
    * setnx()
    * redis集群模式的分布式锁，可以采用redis的Redlock机制
* 基于 ZooKeeper 实现
    * 使用 ZooKeeper 的**临时有序节点**来实现的分布式锁。原理就是：当某客户端要进行逻辑的加锁时，就在zookeeper上的某个指定节点的目录下，去生成一个唯一的临时有序节点， 然后判断自己是否是这些有序节点中序号最小的一个，如果是，则算是获取了锁。如果不是，则说明没有获取到锁，那么就需要在序列中找到比自己小的那个节点，并对其调用exist()方法，对其注册事件监听，当监听到这个节点被删除了，那就再去判断一次自己当初创建的节点是否变成了序列中最小的。如果是，则获取锁，如果不是，则重复上述步骤。当释放锁的时候，只需将这个临时节点删除即可。


## 分布式事务

分布式事务就是在分布式系统中实现事务。

1. 两阶段提交（2PC Two-phase Commit)

2. 3PC

3. TCC (Try-Commit-Cancel)

4. 事务消息

事务消息适用的场景主要是那些需要异步更新数据，并且对数据实时性要求不高的场景。

![事务消息图示](https://static001.geekbang.org/resource/image/27/e6/27ebf12e0dc79e00e1e42c8ff0f4e2e6.jpg)

注意到，上图中，步骤 4 的提交或回滚失败，不通过的 MQ 有不同的处理方式。Kafka 会直接抛出异常，交给 Producer 来处理；RocketMQ 的事物反查机制：

![RocketMQ 的事物反查机制](https://static001.geekbang.org/resource/image/11/7a/11ea249b164b893fb9c36e86ae32577a.jpg)

上述三种实现方法，都有各自的优缺点，适用于不同的场景。

[干货 | 一篇文章带你学习分布式事务](https://mp.weixin.qq.com/s/RDnf637MY0IVgv2NpNVByw)




## 微服务

微服务架构，将庞大臃肿的单体应用拆解开，独立开发，独立部署维护，提高系统的可用性；同时，由不同的小团队负责一个服务，开发迭代速度快。

### 什么是微服务？

* 单体应用的殇

1. 部署效率低下，发布耗时
2. 随着团队规模变大，团队协作成本高
3. 系统在同一个 process 里，高可用性差

* 服务化的出现

* 微服务的出现

### 什么时候适合微服务改造？

* 如何进行服务拆分

1. 纵向拆分（业务维度）
2. 横向拆分（模块维度）

* 服务改造引入和问题

1. 服务如何定义
2. 服务如何发布和订阅
3. 服务如何监控
4. 服务如何治理
5. 故障如何定位


### 微服务架构是怎样的？

* 微服务组件

1. 服务描述
2. 注册中心
3. 服务狂简
4. 服务监控
5. 服务追踪
6. 服务治理
