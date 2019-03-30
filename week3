什么是超线程？ 

什么是CPU socket ？





open打开系统文件的时候

O_direct标识



aio 异步I/O



## Virt-IO



结构：

* 前端： virtio-blk / virtio-net /   guest中的驱动模块
* virtio
* virtio-ring
* virtio-backend 





什么是ring buffer



virt-io是需要guest支持的。 guest的os必须知道自己是虚拟机



**在guest中查看virt-io生效情况**



目前情况：

~~~shell
lsmod | grep virtio
~~~

目前看不见东西， 是否意味着guest中没有对应驱动？



但是



~~~shell
lspci | grep -i block 
~~~

和

~~~sh
lspci -vv -s 00:04.0
~~~

是能看见东西的， 意味着在pci线上的东西是对的吗？











## libvirt — KVM-QEMU管理接口









## 磁盘性能测试工具

DD

IOzone

Bonnie++







### KVM 信息

KVM Forum







## 文件系统

### VFS

只存在在内存中，在系统启动时候建立，关机消亡



## Open系统调用

Sysopen函数



调用栈：

```C
sys_open()->do_sys_open()->do_filp_open()
```

在函数

```c
do_filp_open()
```

中， 有

```c
O_SYNC 
O_DSYNC
o_TRUNC
O_APPEND
```





## QEMU

/v1.c   the main emulator loop. the virtual 



what is TCG ？ 

负载做动态二进制翻译的





main_loop()  /v1.c

和QEMU LOCK的关系 ？




















