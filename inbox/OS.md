
## Zero-Copy
https://bytetech.info/articles/7018806851504439332
### mmap


### sendfile


## 无锁


## epoll, select and poll
先我们需要一个内核为Linux 2.6及以上版本的操作系统，因为Linux 2.6及以上内核才 支持epoll，而在Linux上使用select或poll来解决事件的多路复用，是无法解决高并发压力问题 的。



### Stack and Thread

在 多线程 情况下，每个线程将拥有其自己的完全独立的 **stack** ，但它们将共享 heap 。 stack 是特定于 线程 的，而 heap 是特定于应用程序的。
