# 同步/异步与阻塞/非阻塞

对于进程或线程，有3种状态：运行、就绪、阻塞。

某个进程发起系统调用`read()`，

同步：A发起调用B后，B去执行相应的操作，只有当B操作完成、返回完整的结果后，A才会继续。

异步：A发起调用B后，B立即返回。调用请求可能还未到达B，可能放在缓冲区等待B拿取。调用结果需要B主动通知，或A轮询得到。

阻塞：A发起调用B后，A自身被操作系统挂起，进入阻塞态。

非阻塞：A发起调用B后，B立即返回，A自身并不会进入阻塞态。



可以看到：同步异步更加关注B的状态（操作完成后返回 or 立即返回，轮询 or 主动通知），阻塞非阻塞更关注A的状态（挂起 or 继续运行）。



共有4种组合：

* 同步阻塞：A发起调用后，进入阻塞态。B执行相应操作，直到B返回完整的结果，A才被OS唤醒。
* 同步非阻塞：A发起调用后，B立即返回（如文件描述符），A继续执行其他任务。A不断轮询，直到获取到B返回完整的结果。
* 异步阻塞：A被挂起，B是否主动通知意义不大，几乎不存在。
* 异步非阻塞：A发起调用后，B立即返回，A继续执行其他任务。B完成后主动通知A（如回调函数）。

所以通常来讲，如果提到异步，那一定是非阻塞的。





