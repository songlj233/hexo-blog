# 对Handler的理解

### 基本介绍

Handler消息机制是Android中的事件驱动机制，是用于线程间通讯的一种解决方案，简单说就是在主线程中统一调度各个线程发送的消息。

在应用启动的时候，有一个main函数作为应用的入口，在一个叫ActivityThread的类中，这个main函数中，创建了一个Handler，一起创建的还有Looper，用于消息事件的驱动（Android应用程序启动后没有关闭，也是因为这个Looper创建了一个for(;;)的死循环）。

### 工作流程

介绍工作流程前，要先讲一下配合Handler一起使用的MessageQueue，这是一个消息队列，他是一个按时间排序的优先级队列，他的本质其实就是单向链表。这个消息队列接收Handler发送过来的消息，根据时间节点来确定插入MessageQueue的位置，然后由Looper.loop()取出队头的消息(消息要满足：消息的执行时间≥系统的当前时间),并进行分发调度。

一个线程有且只有一个Looper，在应用启动的时候，通过prepare()函数创建的，保存在ThreadLocal中(ThreadLocal里面有一个ThreadLocalMap，跟HashMap类似的保存键值对)，如果Looper已经存在则不会重复创建，保证了一个线程只能有一个Looper。

但是一个线程可以有多个Handler，但是都对应同一个消息队列，由同一个Looper统一调度。

## 同步屏障机制（选讲）

消息有分同步和异步。当消息需要优先执行时（点击事件，布局绘制），可以发送同步屏障postSyncBarrier，他的本质也是发送一个message，但是这个message的target为null。当消息队列用next获取下一个message的时候，如果消息的target为null，就知道当前有同步屏障，就会遍历消息队列中的异步消息优先执行。如果不需要同步屏障的时候，还需要将它移除。

## 总结

1. AsyncTask他的本质也是使用了Handler的消息机制
2. 使用Handler需要避免内存泄露
3. loop函数死循环，不会anr的原因：消息队列有可以执行的消息才会取出数据并分发消费，没有当前可执行的消息，则会阻塞，进入休眠状态，不消耗资源（阻塞是调用原生的linux层的epool机制，那是一种IO多路复用机制，有新消息就会唤醒）。而anr的原因是主线程的任务在长时间内还没有执行完毕，而消息队列阻塞只是说明当前没有新的消息需要执行，所以这是两码事。而且，主线程的任务其实也是靠消息队列驱动的，比如onCreate()函数等。用一句话总结就是，一个是任务分发，一个是任务消费。
4. 子线程创建looper要经过prepare，loop方法，退出线程要quit，释放资源
5. 参考[Handler的内功心法](https://blog.csdn.net/c10wtiybq1ye3/article/details/111350613)