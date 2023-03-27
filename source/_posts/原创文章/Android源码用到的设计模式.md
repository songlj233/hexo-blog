# Android源码用到的设计模式

## 3种类型

1. 创建型模式5种：单例模式，抽象工厂模式，工厂模式，原型模式，建造者模式
2. 结构型模式7种：适配器模式，桥接模式，装饰模式，组合模式，外观模式，享元模式，代理模式。
3. 行为型模式11种：观察者模式，中介者模式，访问者模式，解释器模式，迭代器模式，备忘录模式，责任链模式，状态模式，策略模式，命令模式，模板模式。

## 23种设计模式及例子（按书本顺序）

1. 单例模式 - getSystemService()获取系统服务
2. 建造者模式 - AlertDialog框的创建
3. 原型模式 - 对象的clone
4. 工厂方法模式 - getSystemService()获取系统服务，Service的onBind
5. 抽象工厂模式 - Service的onBind
6. 策略模式 - 动画插值器
7. 状态模式 - wifi状态
8. 责任链模式 - 点击事件分发
9. 解释器模式 - AndroidManifest.xml文件的解析
10. 命令模式 - 点击事件封装成命令
11. 观察者模式 - Adapter的notifyDataSetChanged()、点击事件的监听、EventBus
12. 备忘录模式 - activyti的onSaveInstanceState
13. 迭代器模式 - java的Iterator，sqlite检索的光标cursor
14. 模版方法模式 - activity的生命周期
15. 访问者模式 - 编译器的注解？
16. 中介者模式 - Binder通信中的ServiceManager和Binder驱动，mvc模式中的C，mvp的p
17. 代理模式 - Binder代理
18. 组合模式 - ViewGroup包含ViewGroup和View
19. 适配器模式 - Listview的Adapter
20. 装饰者模式- ContextImpl
21. 享元模式 - 线程池、Message消息
22. 外观模式 - startActivity()
23. 桥接模式 - Window和WindowManager

参考1. [从Android代码中来记忆23种设计模式](https://www.jianshu.com/p/1a9f571ad7c0)

参考2. 书籍《Android源码设计模式解析与实战》