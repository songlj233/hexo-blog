---
title: 浅谈Binder和AIDL的理解
tags:
  - 原创
  - 安卓
categories:
  - 安卓
abbrlink: 23f8f4e2
date: 2021-01-20 16:52:00
---


## Binder基本概述

Binder主要是用于进程间的通讯，一个Binder通讯要分成客户端和服务端，简单的说就是客户端通过绑定服务端，获取了服务端的IBinder对象，这个IBinder对象，就是代理模式中的那个代理（或者说是c语音中的指针，指向了服务端），然后客户端通过这个代理对象，就可以通过transact方法，向服务端发送数据，实现了进程间的通讯。

## Binder数据传递

这个Binder传递数据的过程，主要就是用到了内存映射。内存映射的意思就像我们电脑上的快捷方式，我们使用的快捷方式，其实也是映射到了真实的文件。在Binder中，就是客户端通过代理对象的transact方法，把数据拷贝到linux内核区域，然后服务端会通过内存映射的方式，获取到那个内核区域中的数据，在onTransact中回调，然后服务端处理并返回，就这样实现了数据的通讯。

## AIDL使用方法

服务端：1.创建接口，2.定义binder，实现接口，3.创建服务，返回binder；

客户端：1.绑定服务，2.实现ServiceConnection绑定监听，3.在绑定成功的回调中，将IBinder转换成AIDL的接口代理对象。

客户端和服务端绑定成功后，就可以通过AIDL的接口代理对象，就像直接调用本地方法一样，调用服务端的方法了。需要注意的是，AIDL间传递的对象要实现Parcelable接口。

## AIDL绑定过程

客户端先调用bindService方法，发起绑定服务的请求，通过ServiceManager，拿到ActivityManagerService，也就是AMS，然后通过AMS向服务端发起bindService的请求。然后服务端接收到绑定请求，以Handler消息机制的方式，发送一个绑定服务的Message，然后在ActivityThread中处理这个绑定请求，调用onBind函数，并返回对应的IBinder对象。这个返回IBinder对象的操作，基本就和绑定过程的通过ServiceManager、AMS类似了。

## AIDL和Binder有什么关系

AIDL的使用实质就是对Binder机制的封装，主要就是将Binder封装成一个代理对象proxy，从用户的角度看，就像是客户端直接调用了服务端的代码。