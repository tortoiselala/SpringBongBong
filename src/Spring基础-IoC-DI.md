# Spring基础

# IoC容器

IoC(Inversion of Control, 控制反转)是Spring容器的核心。什么是控制反转，控制的是什么，又对什么的控制进行反转。
在面向对象的系统设计中，存在“组合”，“继承”等方法，来使得系统的各个组件系统工作，最终实现业务逻辑，这便是对象与对象之间的耦合关系，也可以称之为依赖关系。
1996年，Michael Mattson在一篇有关探讨面向对象框架的文章中，首先提出了IoC 这个概念。简单来说就是把复杂系统分解成相互合作的对象，这些对象类通过封装以后，内部实现对外部是透明的，从而降低了解决问题的复杂度，而且可以灵活地被重用和扩展。
IoC理论提出的大致观点是：借助额外的工具实现具有依赖关系的对象之间的解耦。对于一个对象，我们在自己使用的时候往往是遵循着：创建，使用，销毁这一过程，而这一过程体现了我们对于对象的整个生命周期的控制，我们拥有完整的控制权。
在没有引入Ioc容器之前，对象在初始化或运行到某一点时主动创建或使用已经创建完成的依赖的对象，无论创建还是使用对象，控制权都在自己手上、
在引入Ioc容器后，对于某个对象依赖的对象，容器会自动创建并注入到该对象需要使用的地方。

我理解的控制是对对象创建的控制权，反转则是对控制权的反转：从主动获得对象到由Ioc容器注入。

# DI（Dependency Injection）

   2004年，Martin Fowler探讨了同一个问题，既然IoC是控制反转，那么到底是“哪些方面的控制被反转了呢？”，经过详细地分析和论证后，他得出了答案：“获得依赖对象的过程被反转了”。控制被反转之后，获得依赖对象的过程由自身管理变为了由IoC容器主动注入。于是，他给“控制反转”取了一个更合适的名字叫做“依赖注入（Dependency Injection）”。他的这个答案，实际上给出了实现IoC的方法：注入。所谓依赖注入，就是由IOC容器在运行期间，动态地将某种依赖关系注入到对象之中。
　　所以，依赖注入(DI)和控制反转(IoC)是从不同的角度的描述的同一件事情，就是指通过引入IoC容器，利用依赖关系注入的方式，实现对象之间的解耦。
参考资料：

- Inversion of Control Containers and the Dependency Injection pattern[^1]
- 深度理解依赖注入（Dependence Injection）[^2]
- Object Builder Application Block[^3] 

# 依赖注入的方式

- 构造函数注入
- 属性注入
- 接口注入

Spring的IoC容器通过配置文件的方式找到所需对象（Bean）然后注入到目标位置。

# 参考资料：
- [^1]: Inversion of Control Containers and the Dependency Injection pattern
  [^2]: http://www.cnblogs.com/xingyukun/archive/2007/10/20/931331.html
  [^3]: http://www.cnblogs.com/zhenyulu/articles/641728.html


