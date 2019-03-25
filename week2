# 一些想法



- virtio - blk











2012-forum-virtio-blk-performance-improvement



![virtio-model](/Users/acat/Documents/virtio-model.png)







中间层已经被大幅度打掉了

​	1. 没有两次调度

![](/Users/acat/Documents/virtio-blk2012.png)



支持的内核版本：

● merged blk-mq drivers up to v3.17-rc5

ubuntu 16.4内核 4.4





怎么修改支持：

2012年依然有的问题：



- Virtio-blk-data-plane

- virtio-blk(dataplane) device backend: null_blk

怎么去设置这个东西？





写的思路和想的一样， QEMU支持的处理I/O的线程数目不同会很大的影响写效率。

话说回来：

​	如果有两个QEMU线程在写同一个.img 那么锁的问题是不是就会出现了？





###  QEMU: bypass coroutine



多遍测试读写性能。—> 在不同mode底下

不同mode下写性能的确不一样。



### 为什么？ 不同mode运行的机制到底是什么样？





### qemu ： activate miltiqueue









writethrough

This mode causes the hypervisor to interact with the disk image file or block device with `O_DSYNC` semantics. Writes are reported as completed only when the data has been committed to the storage device. The host page cache is used in what can be termed a writethrough caching mode. The guest's virtual storage adapter is informed that there is no writeback cache, so the guest would not need to send down flush commands to manage data integrity. The storage behaves as if there is a writethrough cache.





### qemu **dataplane**























































 

 

