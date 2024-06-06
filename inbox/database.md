---
layout: lecture
title: "Database Basic"
date: 2022-07-11
ready: true
---

#### 关系型数据库 MySQL

**sql的执行顺序**

from -> where -> group by -> having -> select -> order by -> limit

**数据库引擎**

最常用的是MyISAM与InnoDB，

* MYISAM： 不支持事物; 适合查询以及插入为主的应用; 不支持外键
* INNODB： 支持事物; 频繁修改以及涉及到安全性较高的应用; 支持外键; InnoDB是用B+树来建立索引的

在MySQL 5.5版本以前，MyIASM是MySQL默认的存储引擎, 而在MySQL 5.5之后，默认的存储引擎为InnoDB

**MySQL 表格设计**

**mysql表设计原则(三个范式)**

1. 第一范式: 每列保持原子性

每一列都不可拆分

1. 第二范式: 每列都和主键相关

在第一范式的基础之上更进一步，第二范式确保表格中每一列都要和主键有关, 如何存在复合主键的，需要依赖整个复合主键，而不是其中一部分主键，否则就拆分表格

1. 第三范式: 每列都和主键列直接相关,而不是间接相关

比如A是主键，B依赖于A，C依赖于B，这时候需要对ABC拆分成两个表格

**B树 vs B+树**

B+树最高可以有几层

B+树的层高的计算 (文章很不错)

[https://juejin.cn/post/6904293886626103309](https://juejin.cn/post/6904293886626103309)

需要注意的是，数据库里面的数据转换是以page为单位来进行读写的

**MongoDB 使用B树**

[https://segmentfault.com/a/1190000041201491#:\~:text=MySQL](https://segmentfault.com/a/1190000041201491) 使用B%2B 树是,可以接受的时延。

**二叉树 红黑树 B树 B+树**

[https://blog.csdn.net/jinking01/article/details/115537954](https://blog.csdn.net/jinking01/article/details/115537954)

**Recommend reading**

[https://juejin.cn/post/6844904096378404872](https://juejin.cn/post/6844904096378404872)

**MySQL 事务处理**

[https://www.cnblogs.com/kismetv/p/10331633.html](https://www.cnblogs.com/kismetv/p/10331633.html)

**MySQL架构**

校验器、解释器、优化器、执行器

**事务管理**

关系型数据库中，事务管理是重要的一环。另外，大多数的非关系型数据库是没有事务管理的能力。

**事务管理(ACID)**

[https://blog.csdn.net/qq\_32690999/article/details/78007621](https://blog.csdn.net/qq\_32690999/article/details/78007621)

**1. 原子性（Atomicity）**

原子性是指事务是一个不可分割的工作单位，事务中的操作要么都发生，要么都不发生。如果事务中一个sql语句执行失败，则已执行的语句也必须**回滚**，数据库退回到事务前的状态。

原子性是通过undo log来保持

**2. 一致性（Consistency)**

事务前后数据的完整性必须保持一致。

原子性，隔离性和持久性都是用来保证一致性

**3. 隔离性（Isolation）**

事务的隔离性是多个用户并发访问数据库时，数据库为每一个用户开启的事务，不能被其他事务的操作数据所干扰，多个并发事务之间要相互隔离。

这个应该比较复杂，通过锁，MVCC，RR等机制来实现隔离性

**4. 持久性（Durability)**

持久性是指一个事务一旦被提交，它对数据库中数据的改变就是永久性的，接下来即使数据库发生故障也不应该对其有任何影响

使用redo log来保证事务的持久性

**理解事务的4种隔离级别**

MySQL的NDB Cluster事务不满足持久性和隔离性；InnoDB默认事务隔离级别是可重复读，不满足隔离性；Oracle默认的事务隔离级别为READ COMMITTED，不满足隔离性

**BinLog，RedoLog，UndoLog**

**数据库索引**

**hash索引**

[https://blog.csdn.net/weixin\_43767015/article/details/119346481#:\~:text=730-,%E5%93%88%E5%B8%8C%E7%B4%A2%E5%BC%95%EF%BC%88hash%20index%EF%BC%89%E5%9F%BA%E4%BA%8E%E5%93%88%E5%B8%8C%E8%A1%A8%E5%AE%9E%E7%8E%B0,%E6%9F%A5%E6%89%BE%E7%9A%84%E9%80%9F%E5%BA%A6%E9%9D%9E%E5%B8%B8%E5%BF%AB%E3%80%82](https://blog.csdn.net/weixin\_43767015/article/details/119346481)

[https://segmentfault.com/a/1190000023314270](https://segmentfault.com/a/1190000023314270) [https://blog.csdn.net/m0\_37204491/article/details/72852996](https://blog.csdn.net/m0\_37204491/article/details/72852996)

* 聚集索引和非聚集索引

索引分为**聚簇索引**(cluster)和**非聚簇索引**(uncluster)两种，[聚簇索引](https://so.csdn.net/so/search?q=%E8%81%9A%E7%B0%87%E7%B4%A2%E5%BC%95\&spm=1001.2101.3001.7020)是按照数据存放的物理位置为顺序的，而非聚簇索引就不一样了；聚簇索引能提高多行检索的速度，而非聚簇索引对于单行的检索很快。(really ?)

[https://blog.csdn.net/wh445306/article/details/122237039](https://blog.csdn.net/wh445306/article/details/122237039)

* 索引失效

常见的索引失效情况有:

* or语句前后没有同时使用索引。当or左右查询字段只有一个是索引，该索引失效，只有当or左右查询字段均为索引时，才会生效
* 复合索引未用左列字段，即不是使用第一列索引，索引失效
* like以%开头的时候失效。但是当like前缀没有%，后缀有%时，索引是有效的
* where中在索引字段上使用not，<>，!=, 因为不等于操作符不会用到索引
* 如何过mysql优化器发现全扫描更快，就不会用索引
* 在索引列上使用 IS NULL 或 IS NOT NULL操作。原因是索引是不索引空值的，所以这样的操作不能使用索引
* 最左匹配

最左匹配原则都是针对联合索引的, 以最左边的为起点任何连续的索引都能匹配上。同时遇到范围查询就会停止匹配。

从这里还可以引出排序算法稳定性的问题

常见的锁以及其问题

[https://juejin.cn/post/6844903974307364877](https://juejin.cn/post/6844903974307364877)

[https://cloud.tencent.com/developer/article/1803387](https://cloud.tencent.com/developer/article/1803387)

乐观锁和悲观锁

CAS算法

[https://zhuanlan.zhihu.com/p/34556594](https://zhuanlan.zhihu.com/p/34556594)

mysql支持的锁

[https://segmentfault.com/a/1190000023869573#:\~:text=MySQL%E6%94%AF%E6%8C%81%E4%B8%8D%E5%90%8C%E7%BA%A7%E5%88%AB%E7%9A%84,%E6%98%AF%E9%87%87%E7%94%A8%E8%A1%8C%E7%BA%A7%E9%94%81%E3%80%82](https://segmentfault.com/a/1190000023869573)

sql语句对表加锁 这里是写sql语句 类似于我们常见的查成绩之类 不太难 但是会问你加的什么锁 保证了什么机制

[https://juejin.cn/post/7096789207502290951](https://juejin.cn/post/7096789207502290951)

数据库事务 以及相应的隔离级别 分别解决什么问题？

[https://developer.aliyun.com/article/743691](https://developer.aliyun.com/article/743691)

mvcc能不能解决幻读

[https://mp.weixin.qq.com/s/ZVsuqpaKTAMeA0SyqRbqyw](https://mp.weixin.qq.com/s/ZVsuqpaKTAMeA0SyqRbqyw) (这一篇很不错)

[https://juejin.cn/post/7092056967216119845](https://juejin.cn/post/7092056967216119845)

[https://blog.csdn.net/qq\_35590091/article/details/107734005](https://blog.csdn.net/qq\_35590091/article/details/107734005)

间隙锁 [https://cloud.tencent.com/developer/article/1806998#:\~:text=%E9%97%B4%E9%9A%99%E9%94%81%EF%BC%88Gap%20Lock%EF%BC%89%EF%BC%9A,%E2%80%9C%E9%97%B4%E9%9A%99%EF%BC%88GAP%EF%BC%89%E2%80%9D%E3%80%82](https://cloud.tencent.com/developer/article/1806998)

乐观锁和悲观锁的应用场景

[https://blog.csdn.net/ahjxhy2010/article/details/80519664](https://blog.csdn.net/ahjxhy2010/article/details/80519664)

innodb数据引擎 (非常好的文章)

[https://juejin.cn/post/6844904190477598733](https://juejin.cn/post/6844904190477598733)

**RR隔离级别能否保证不出现幻读**

**MySQL的MVCC**

Multi-Version Concurrency Control，即多版本的并发控制协议

[https://segmentfault.com/a/1190000037557620](https://segmentfault.com/a/1190000037557620)

[https://blog.csdn.net/SnailMann/article/details/94724197](https://blog.csdn.net/SnailMann/article/details/94724197)

#### 非关系型数据库

**MongoDB**

数据存储在硬盘中，面向文档的数据库

**Redis**

* 数据存储在内存中，有持久化机制来放丢失
* key-value的数据库
* 缓存穿透、缓存雪崩、缓存击穿 以及各自的解决方案
* 持久化：AOF和RDB： [https://developer.aliyun.com/article/541097#:\~:text=RDB](https://developer.aliyun.com/article/541097)持久化是指,到详细的操作记录。
* skiplist： 为什么使用跳表[https://www.zhihu.com/question/20202931](https://www.zhihu.com/question/20202931)
* 延迟双删

**建立索引的原则**

**关系型数据库 建立索引**

[https://cloud.tencent.com/developer/article/1426776](https://cloud.tencent.com/developer/article/1426776)

**非关系型数据 建立索引**

**Learning Redis**

缓存中间级，消息队列中间件

**超大规模数据如何用redis来存储：**

需要考虑的问题：

1. 长短不一容易造成内存碎片
2. 由于指针大量存在，内存膨胀率比较高，一般在7倍，纯内存存储通病；
3. 虽然可以通过cookie的行为预判其热度，但每天新生成的id依然很多
4. 由于服务要求在公网环境（国内公网延迟60ms以下）下100ms以内，所以原则上当天新更新的mapping和人口标签需要全部in memory，而不会让请求落到后端的冷数据；
5. 业务方面，所有数据原则上至少保留35天甚至更久；

解决方案：

1. 淘汰策略
2. 减少膨胀
3. 减少碎片

缓存击穿，缓存穿透，缓存雪崩，以及它们的解决方案。

[https://zhuanlan.zhihu.com/p/91539644](https://zhuanlan.zhihu.com/p/91539644)

redis 持久化的方式(RDB, AOF)

Redis我看你也有了解，你介绍一下它的有几种数据类型？详细说一下

为什么Redis会比Mysql快？

1）Redis是基于内存存储的，而mysql是基于磁盘存储的，内存的交互肯定是要比磁盘的交互快的

2）Redis内数据存储格式是KV形式查找数据时的时间复杂度是O(1)，Mysql底层是B+树，查找数据时的时间复杂度是O(logN)所以查找数据时Redis是比Mysql要快的

3）Redis是单线程多路复用IO，单线程的切换的话他避免的线程切换消耗的时间，多路复用IO避免了IO等待的开销

#### 分布式数据库

**一致性哈希**

为什么会有一致性哈希？ 首先我们来看一下传统hash的问题，如果hash对应的bucket的数量固定了，这时候如果新增一个bucket需要rehash。 有了一致性哈希，就可以解决rehash的问题

数据倾斜问题？ 一致性哈希可能存在数据倾斜问题，解决方案是用虚拟节点

## 面试中的数据库知识

#### 什么情况下要创建索引

* 在经常需要搜索的列上，可以加快搜索的速度。
* 在作为主键的列上，强制该列的唯一性和组织表中数据的排列结构。
* 在经常用于连接两张表的列上，这些列主要是一些外键，可以加快连接的速度。
* 在经常需要根据范围进行搜索的列上创建索引，因为索引已经排序，其指定的范围是连续的。
* 在经常需要排序的列上创建索引，因为索引已经排序，这样查询可以利用索引的排序，加快排序查询时间。
* 在经常使用在WHERE子句中的列上面创建索引，加快条件的判断速度。

#### 什么情况下不适合创建索引

* 表记录太少。
* 经常增删改的表。
* 数据重复且分布平均的表字段，因此应该只为最经常查询和经常排序的数据列建立索引（如果某个数据列包含许多重复的内容，为它建立索引就没有太大的实际效果）。

#### 什么时候索引失效

[https://blog.csdn.net/bless2015/article/details/84134361](https://blog.csdn.net/bless2015/article/details/84134361)

#### 介绍下数据库的索引以及作用

[https://blog.csdn.net/u013310119/article/details/52527632](https://blog.csdn.net/u013310119/article/details/52527632)

**数据库的存储引擎，介绍一下，以及其数据结构**

[https://blog.csdn.net/IPI715718/article/details/98478419](https://blog.csdn.net/IPI715718/article/details/98478419)

#### 什么是 B+树

#### 数据库的事务以及特点

[http://c.biancheng.net/view/7289.html](http://c.biancheng.net/view/7289.html)

原子性（Atomicity）、一致性（Consistency）、隔离性（Isolation）和持久性（Durability）

**写sql语句，group by**

**为什么需要rollback**

还是去看看db课件吧

**MySQL不同引擎的区别**

[https://blog.csdn.net/printwsl/article/details/80058841](https://blog.csdn.net/printwsl/article/details/80058841)

**不同引擎的索引区别（索引的底层实现）**

[https://blog.csdn.net/cy973071263/article/details/104513633](https://blog.csdn.net/cy973071263/article/details/104513633)

[https://blog.csdn.net/k393393/article/details/100027666](https://blog.csdn.net/k393393/article/details/100027666)

**存储过程**

[https://blog.csdn.net/lck898989/article/details/78697657](https://blog.csdn.net/lck898989/article/details/78697657)

**MySQL的多线程并发是怎么做的**

[https://blog.csdn.net/qq\_35044419/article/details/82592187](https://blog.csdn.net/qq\_35044419/article/details/82592187)

**MySQL线程池怎么设计的**

[https://blog.csdn.net/weixin\_44189883/article/details/85127723](https://blog.csdn.net/weixin\_44189883/article/details/85127723)

**innodb和mylsam的异同**

InnoDB 是 MySQL 中第一个提供外键约束的存储引擎，而且它对事务的处理能力是其它存储引擎无法与之相比的。

**MyISAM**是[MySQL](https://baike.baidu.com/item/MySQL)的默认[数据库引擎](https://baike.baidu.com/item/%E6%95%B0%E6%8D%AE%E5%BA%93%E5%BC%95%E6%93%8E)

[https://blog.csdn.net/qq\_35642036/article/details/82820178](https://blog.csdn.net/qq\_35642036/article/details/82820178)
