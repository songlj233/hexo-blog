# Activity启动流程

## 发送启动Activity的请求

点击桌面的图标，其实就是在launcher这个应用中，调用Context的startActivity方法，Context的具体实现是在ContextImpl中，从这个实现类中可以看到，又通过Instrumentation来启动Activity。在Instrumentation中，通过Binder进程间通讯的方式，获取了AMS的Binder对象，通过这个Binder对象，向AMS发起启动activity的请求。

## AMS处理请求

然后就是AMS处理请求了，AMS会调用PMS，校验即将启动的Activity的相关参数，比如解析传入的intent信息，还有activity的合法性，还有启动模式等，另外还有activity的栈信息的相关处理。解析正常后，让当前栈顶的Activity执行onPause，然后开始正式启动Activity了。

## 创建进程（如果应用未创建）

如果应用没有启动，则需要执行创建应用的过程，具体就是通过ams，以socket的形式，去通知zygote去fork出一个新的子进程，这里用了socket，而不是用binder（因为用binder就相当于有子进程，fork的时候有子线程会造成死锁），这个创建出来的子进程执行ActivityThread.main方法，这个main方法就是这个应用的入口，主要做各种的初始化操作，包括application、handler、looper等。

## 真正启动Activity

然后才是真正的启动activity。由AMS通过持有的我们应用的Binder引用，也就是ApplicationThread对象，向我们的应用发起启动Activity的通知。因为是通过Binder的通信方式接受消息的，所以需要通过Handler的消息机制，从Binder线程切换到UI线程。

然后启动的主要流程就是平时所说的Activity的生命周期了。在执行对应生命周期时，还会通过Fragment控制器，通知对应Fragment生命周期的变化。（9.0及以后的版本使用状态机的设计模式管理Activity的生命周期）。

## 附图

7.0版本的Activity启动时序图

![Activity%E5%90%AF%E5%8A%A8%E6%B5%81%E7%A8%8B%20de1aa1b36a0b44c4907f5e2ef5bbef6e/Untitled.png](Activity%E5%90%AF%E5%8A%A8%E6%B5%81%E7%A8%8B%20de1aa1b36a0b44c4907f5e2ef5bbef6e/Untitled.png)

9.0版本的Activity启动时序图：

![Activity%E5%90%AF%E5%8A%A8%E6%B5%81%E7%A8%8B%20de1aa1b36a0b44c4907f5e2ef5bbef6e/Untitled%201.png](Activity%E5%90%AF%E5%8A%A8%E6%B5%81%E7%A8%8B%20de1aa1b36a0b44c4907f5e2ef5bbef6e/Untitled%201.png)

## 参考

[Android 重学系列 Activity的启动流程(一)](https://www.jianshu.com/p/91feec107d4b)

[Android 重学系列 Activity的启动流程(三)](https://www.jianshu.com/p/ac7b6a525b96)