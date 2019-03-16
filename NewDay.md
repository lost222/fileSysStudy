# 一些问题

写在最前： idea是什么？ 和这篇论文哪些部分相关？



idea： 虚拟机对**多文件**的读写， 表现为宿主机上多个计算单元（假如我把进程绑定在CPU核心上， 它怎么对应宿主机？）对单个img文件的读写。 这因为锁的问题， 可能会很慢



论文相关的一些概念：

- Sharing Level : 单文件读写或者多文件读写

For reading data blocks, FXMARK provides three benchmarks based on the sharing level: 

(1) reading a data block in the *private file* of a benchmark process (low),

 (2) reading a *private data block* in the *shared file* among benchmark processes (medium)

(3) reading the *same data block* in the shared file (high).









- 为什么要有Runner.NVMEDEV, Runner.LOOPDEV？





/dev/loop 里哪一个是mem ？ 为什么需要测试mem ？



- 到底什么是多核？ 多核怎么体现到代码里的？ 如果我创建超过核心数目的线程， 情况是如何？ 

  Note that we use processes instead of threads, to avoid a few known scalability bottlenecks (e.g., allocating file descriptors and virtual memory management) in the Linux kernel [21, 33].

  目前的情况是只能检测 2 核心的状况。 我可以尝试绕过监测CPU核心数目， 和将进程绑定在CPU核心上的代码，但是我不确定这样还是不是满足控制变量。   （论文里谈到已经有一些众所周知的多线程瓶颈）

  





## 他提出的什么东西对我有用：

- many core performance depends on filesystem rather than storage mediums

  

  

  

  

  

## 我做了一些什么？

HDD

模式： DWOL ， Overwrite a block in a private file（目前最接近我们idea的模式）

- 宿主机在各个文件系统下的scability， 只有两个核心！

  - directio
  - bufferedio

- 虚拟机在各个文件系统下的scability， 有四个核心？ 不明白为什么是4个

  img文件在宿主机的ext4文件系统下

  - directio
  - bufferedio



SSD

模式： DWOL ， Overwrite a block in a private file（目前最接近我们idea的模式）

- 宿主机在各个文件系统下的scability， 只有两个核心！

  - directio
  - bufferedio

- 虚拟机在各个文件系统下的scability， 有四个核心？ 不明白为什么是4个

  img文件在宿主机的ext4文件系统下

  - directio
  - bufferedio





为什么在有4个VCPU的虚拟机它只探测到一个核心？

无论如何， 我找到方法绕过了它检测CPU数量的过程， 现在我创建的是多进程运行， 这样控制变量做的不好的数据说服力可能没有那么强

 



## 实验计划

- 做完4核心下， 比较scability问题。
- 考虑等价表现情况 虚拟机的DWOL —> 宿主机的 DWOM
- 
- k







## 前进方向

- 假设真的类似 share file privatre block， 现在这类问题的文件系统表现如何， 瓶颈在哪里？ 
- 







## 遇到问题

1. 代码文档不清楚。想要把代码安装我想要的配置跑起来，只能阅读源代码。
   - CPU核心数量的探测是在make过程中完成的。参数保存在 `cpupol.py`中。
   - 文章中谈到他根据CPU核心数量设定进程， 现在我们指定了多于核心数量的进程数目，中间会一些其他的瓶颈干扰， 数据说服力可能有问题。
     - 21
     - 33
2. 数据和想象的不同， 在SSD下， 0-4核下，

宿主机情况

![]()

1. directio 与 bufferedio 扩展性都有差别（无论是在宿主机还是虚拟机） ，都是bufferedio的可扩展性更好

2. bufferedio下，虚拟机和宿主机的表现类似，

   现象描述：

   1. 总的来说， bufferedio下， 虚拟机的整体性能和宿主机在同一个数量级， 符合我们上一篇论文的结果。
   2. 就4核能够看见的情况来说， 虚拟机和宿主机的可扩展性趋势一致。

   理论分析：

   ​	bufferedio下， 虚拟机多文件写是先写入page cache， 到触发os统一将page cache刷回。和我们idea里的情况不一致。

3. directedio下，

   现象描述

   1. 总的来说， directio下，虚拟机的表现比宿主机整体都差了两个数量级，无论是什么文件系统
   2. 宿主机下， f2fs在1核到2核的时候表现出了良好的可扩展性， 同比在虚拟机下是没有的。 

   理论分析

   - 和预期相同：directio下，虚拟机的多核写多文件， 最后会变成宿主机下多核写单个文件。整体性能变差和我们预期相同。
   - 新的问题： 
     - 为什么directio下， 宿主机的多核写多文件也表现不出好的可扩展性？这和many core文章结论不符。
     - 为什么f2fs在宿主机表现出了一定的可扩展性， 但是在虚拟机上没有？

















## 尝试绕过绑定进程到核心的代码







http://pgbovine.net/PhD-memoir.htm

















































































































