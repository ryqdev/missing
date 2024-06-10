

##  What is MQ
MQ(message queue)，本质是个队列，FIFO 先入先出，只不过队列中存放的内容是 message 
已，还是一种跨进程的通信机制，用于上下游传递消息。
在互联网架构中，MQ 是一种非常常见的上下游“逻辑解耦+物理解耦”的消息通信服务。使用了 MQ 之后，消息发送上游只需要依赖 MQ，不用依赖其他服务。


## Why MQ

- 流量消峰
- 应用解耦
- 异步处理


## The Types of MQ
### Rocket MQ


字节内部的rocket mq：https://code.byted.org/rocketmq/rocketmq-go-proxy

### Kafka



### RabbitMQ



### ZeroMQ


### ActiveMQ


## Others
### dbus
https://zh.wikipedia.org/wiki/D-Bus

###  如何发送延迟mq
一般mq是会立即发送消息的，如果需要设定一个时间，比如等过了10min之后再发送消息：
https://juejin.cn/post/7052894117105238053
https://cloud.tencent.com/developer/article/1878229



### Raft
https://thesecretlivesofdata.com/raft/



# Kafka in action

https://www.cnblogs.com/edisonchou/p/kafka_study_notes_part2.html




## Reference
https://juejin.cn/post/7134967327996526605
https://rocketmq.apache.org/zh/docs/


[]()https://kafka.apache.org/intro