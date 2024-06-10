# System Design


### Basic Knowledge


[https://github.com/donnemartin/system-design-primer](https://github.com/donnemartin/system-design-primer)


Everything is a trade-off


#### Performance vs scalability


[https://www.allthingsdistributed.com/2006/03/a_word_on_scalability.html](https://www.allthingsdistributed.com/2006/03/a_word_on_scalability.html)

  


[https://www.slideshare.net/jboner/scalability-availability-stability-patterns/](https://www.slideshare.net/jboner/scalability-availability-stability-patterns/)

  


* Performance: how users feel about the service

* Scalability: how the service performs under heavy load

  


#### Latency vs throughput

  


In the Internet industry, we care about throughput, while in the quant world, we focus on latency.

  


#### Availability vs consistency

  


CAP theory: [https://robertgreiner.com/cap-theorem-revisited/](https://robertgreiner.com/cap-theorem-revisited/)

  


### DNS (Domain name system)

  


[https://www.slideshare.net/srikrupa5/dns-security-presentation-issa](https://www.slideshare.net/srikrupa5/dns-security-presentation-issa)

  


### CDN (Content delivery network)

  


### Load balancer

  


### Reverse proxy (webserver)

  


### Sharding

  


### NoSQL

  


消息中间件的作用 以及具体分类 如何传递消息

  


[https://juejin.cn/post/7063722998477357093](https://juejin.cn/post/7063722998477357093)

  


#### Cases

  


**消息队列**

  


[https://www.zhihu.com/question/54152397](https://www.zhihu.com/question/54152397)

  


**设计排行榜**

  


设计一个排行榜，百万数量级，支持按照score插入，按照uid查找排名，按照名次查找uid redis的zset，保证分布式一致（所有服务器访问同一个排行榜 zrange，zrank，zscore等命令原生支持

  


#### 布隆过滤

  


[https://cloud.tencent.com/developer/article/1974845](https://cloud.tencent.com/developer/article/1974845)

  


[https://juejin.cn/post/6844904007790673933](https://juejin.cn/post/6844904007790673933)

  


**异步 如何处理高并发**

  


[https://juejin.cn/post/6990307911117307934](https://juejin.cn/post/6990307911117307934)

  


[https://blog.51cto.com/u_14410880/2552228](https://blog.51cto.com/u_14410880/2552228)

  


[https://juejin.cn/post/6844903639253794824](https://juejin.cn/post/6844903639253794824)

  


**负载均衡**

  


[https://dubbo.apache.org/zh/docs/v2.7/dev/source/loadbalance/#:~:text=LoadBalance%20%E4%B8%AD%E6%96%87%E6%84%8F%E6%80%9D%E4%B8%BA%E8%B4%9F%E8%BD%BD,%E5%8F%AF%E4%BB%A5%E9%81%BF%E5%85%8D%E8%B5%84%E6%BA%90%E6%B5%AA%E8%B4%B9%EF%BC%8C%E4%B8%80%E4%B8%BE%E4%B8%A4%E5%BE%97%E3%80%82](https://dubbo.apache.org/zh/docs/v2.7/dev/source/loadbalance/)

  


**令牌桶**

  


[https://cloud.tencent.com/developer/news/687927](https://cloud.tencent.com/developer/news/687927)

  


**token bucket vs leaky bucket**

  


redis的适用场景

  


[https://cloud.tencent.com/developer/article/1867518](https://cloud.tencent.com/developer/article/1867518)

  


场景设计题 高并发的场景下如和设计redis的服务器分布 是用什么数据结构 如何设计缓存

  


[https://juejin.cn/post/6844904178087804935](https://juejin.cn/post/6844904178087804935)

  


[https://cloud.tencent.com/developer/article/1976158](https://cloud.tencent.com/developer/article/1976158)

  


[https://juejin.cn/post/7044366350654898207](https://juejin.cn/post/7044366350654898207)

  


redis分布式式锁怎么实现？

  


[https://www.51cto.com/article/688179.html](https://www.51cto.com/article/688179.html)

  


[https://juejin.cn/post/6844903830442737671](https://juejin.cn/post/6844903830442737671)

  


redis分布式事务的原子性怎么保证？是由哪一个机器进行调配？最终一致性怎么保证了？（真的把我问穿了 没用过 只背八股文真没用 要理解 已经开始胡乱编造了）

  


[https://zq99299.github.io/note-book/back-end-storage/01/05.html#_2pc-%E8%AE%A2%E5%8D%95%E4%B8%8E%E4%BC%98%E6%83%A0%E5%88%B8%E7%9A%84%E6%95%B0%E6%8D%AE%E4%B8%80%E8%87%B4%E6%80%A7%E9%97%AE%E9%A2%98](https://zq99299.github.io/note-book/back-end-storage/01/05.html#_2pc-%E8%AE%A2%E5%8D%95%E4%B8%8E%E4%BC%98%E6%83%A0%E5%88%B8%E7%9A%84%E6%95%B0%E6%8D%AE%E4%B8%80%E8%87%B4%E6%80%A7%E9%97%AE%E9%A2%98)

  


[https://juejin.cn/post/7086849924377083918](https://juejin.cn/post/7086849924377083918)

  



