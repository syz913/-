#### Chapter 10

- [文件锁](#文件锁)
- [权限设置](#权限设置)

##### 文件锁

> [参考链接](<https://www.ibm.com/developerworks/cn/linux/l-cn-filelock/index.html>)

###### advisory lock:

劝告锁是一种协同工作的锁。对于这一种锁来说，内核只提供加锁以及检测文件是否已经加锁的手段，但是内核并不参与锁的控制和协调。也就是说，如果有进程不遵守“游戏规则”，不检查目标文件是否已经由别的进程加了锁就往其中写入数据，那么内核是不会加以阻拦的。因此，劝告锁并不能阻止进程对文件的访问，而只能依靠各个进程在访问文件之前检查该文件是否已经被其他进程加锁来实现并发控制。进程需要事先对锁的状态做一个约定，并根据锁的当前状态和相互关系来确定其他进程是否能对文件执行指定的操作。从这点上来说，劝告锁的工作方式与使用信号量保护临界区的方式非常类似。

劝告锁可以对文件的任意一个部分进行加锁，也可以对整个文件进行加锁，甚至可以对文件将来增大的部分也进行加锁。由于进程可以选择对文件的某个部分进行加锁，所以一个进程可以获得关于某个文件不同部分的多个锁。

###### mandatory lock:

与劝告锁不同，强制锁是一种内核强制采用的文件锁，它是从 System V Release 3 开始引入的。每当有系统调用 open()、read() 以及write() 发生的时候，内核都要检查并确保这些系统调用不会违反在所访问文件上加的强制锁约束。也就是说，如果有进程不遵守游戏规则，硬要往加了锁的文件中写入内容，内核就会加以阻拦

##### 权限设置

- ##### Mode of access: read, write, execute

- ##### Three classes of users

  ​                                                                RWX (4, 2, 1)

  - owner access        7               1 1 1
  - group access         6               1 1 0
  - public access         1               0 0 1

```
chmod 761 game // 定义game文件的访问权限
```

#### Chapter 11

##### File

- logical storage unit

- collection of related information

##### File system resides on secondary storage (disks)

- Provieds user inteface to storage, mapping logical to physical
- provides efficent and convenient

##### Efficiency and Performance

Efficiency dependent on:

- Disk allocation and directory algorithm
- Types of data kept in file's directory entry
- pre-allocation or as-needed allocation of metadata structures
- fixed-size or varying-size data structures

Performance

- keeping data and metadata close together
- buffer cache — separate section of main memory for frequently
- synchronous writes sometimes requested by apps or needed by OS
  - No buffering/caching — writes must hit disk before acknowledgement
  - Asynchronous writes more common, buffer-able, faster
- Free-behind and read-ahead — techniques to optimize sequential access
- Reads frequently slower than writes

  

页大小和帧大小相同：实现分页的基本方法涉及将物理内存分为固定大小的块，称为帧或页帧，而将逻辑内存也分为同样大小的块，称为页或页面。