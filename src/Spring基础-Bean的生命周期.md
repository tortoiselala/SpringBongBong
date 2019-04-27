# Bean的生命周期

Bean生命周期由多个特定的生命阶段组成，每个生命阶段都允许外界对Bean施加控制。在Spring

## BeanFactory遵循的标准Bean生命周期接口

首先看一下`BeanFactory`文档中规定的标准的`BeanFactory`应该遵循的Bean生命周期接口与标准顺序：

1. `BeanNameAware`#`setBeanName`

2. `BeanClassLoaderAware`#`setBeanClassLoader`

3. `BeanFactoryAware`#`setBeanFactory`

4. `EmbeddedValueResolverAware`#`setEmbeddedValueResolver`

5. `EnviromentValueResolverAware`#`setEmbeddedValueResolver`

   6-10 只有运行在程序上下文中可用

6. `ResourceLoaderAware`#`setResourceLoader`

7. `ApplicationEventPublisherAware`#`setApplicationEventPublisher`

8. `MessageSourceAware`#`setMessageSource`

9. `ApplicationContextAware`#`setApplicationContext`

10. `ServletContextAware`#`setServletContext` 

11. `BeanPostProcessors`#`postProcessBeforeInitialization`

12. `InitializingBean`#`afterPropertiesSet`

13. 自定义init-method

14. `BeanPostProcessors`#`postProcessAfterInitialization`

关闭`BeanFactory`时，应该遵循如下的顺序：

1. `DestructionAwareBeanPostProcessors`#`postProcessBrforeDestruction`
2. `DisposableBean`#`destory`
3. 自定义destory-method

上面展示了一个`BeanFactory`的实现必须遵循的Bean初始化方法和销毁方法执行顺序.

## BeanFactory中Bean的生命周期

Bean生命周期伴随着一系列的相关事件，BeanFactory根据上面的标准顺序检查注册的事件，并调用。

### Bean生命周期事件种类

Spring容器管理着Bean，决定着Bean的一切，管理过程通过一系列回调函数实现，这些回调函数能够被分为两种：

- **Post initialization**回调函数
- **Pre destruction**回调函数

### Bean生命周期回调函数

Spring framework提供了如下四种管理Bean生命周期事件的途径：

1. `InitializingBean`和`DisposableBean`回调接口
2. 针对特殊需求的`*Aware`接口
3. 配置文件自定义的`init()`和`destroy()`方法
4. `@PostConstruct`和`@PreDestroy`注解

#### `*Aware`接口

Spring提供了一系列的`*Aware`接口使得Bean能够告诉容器其所需的基础依赖。每个接口都要求实现一个方法来向Bean注入依赖。

接口列表如下：

| AWARE INTERFACE                  | METHOD TO OVERRIDE                                           | PURPOSE                                                      |
| -------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| `ApplicationContextAware`        | void `setApplicationContext` (ApplicationContext applicationContext) throws BeansException; | Interface to be implemented by any object that wishes to be notified of the `ApplicationContext` that it runs in. |
| `ApplicationEventPublisherAware` | void `setApplicationEventPublisher`(ApplicationEventPublisher applicationEventPublisher); | Set the `ApplicationEventPublisher` that this object runs in. |
| `BeanClassLoaderAware`           | void `setBeanClassLoader` (ClassLoader classLoader);         | Callback that supplies the bean class loader to a bean instance. |
| `BeanFactoryAware`               | void `setBeanFactory` (BeanFactory beanFactory) throws BeansException; | Callback that supplies the owning factory to a bean instance. |
| `BeanNameAware`                  | void `setBeanName`(String name);                             | Set the name of the bean in the bean factory that created this bean. |
| `BootstrapContextAware`          | void `setBootstrapContext` (BootstrapContext bootstrapContext); | Set the BootstrapContext that this object runs in.           |
| `LoadTimeWeaverAware`            | void `setLoadTimeWeaver` (LoadTimeWeaver loadTimeWeaver);    | Set the LoadTimeWeaver of this object’s containing ApplicationContext. |
| `MessageSourceAware`             | void `setMessageSource` (MessageSource messageSource);       | Set the MessageSource that this object runs in.              |
| `NotificationPublisherAware`     | void `setNotificationPublisher` (NotificationPublisher notificationPublisher); | Set the NotificationPublisher instance for the current managed resource instance. |
| `PortletConfigAware`             | void `setPortletConfig` (PortletConfig portletConfig);       | Set the PortletConfig this object runs in.                   |
| `PortletContextAware`            | void `setPortletContext` (PortletContext portletContext);    | Set the PortletContext that this object runs in.             |
| `ResourceLoaderAware`            | void `setResourceLoader` (ResourceLoader resourceLoader);    | Set the ResourceLoader that this object runs in.             |
| `ServletConfigAware`             | void `setServletConfig` (ServletConfig servletConfig);       | Set the ServletConfig that this object runs in.              |
| `ServletContextAware`            | void `setServletContext` (ServletContext servletContext);    | Set the ServletContext that this object runs in.             |

#### `InitializingBean`和`DisposableBean`回调接口

`org.springframeword.beans.factory.InitalizingBean`接口允许容器将Bean所有必须的属性设置完毕后进行初始化工作。

```java
package org.springframework.beans.factory;
public interface InitializingBean {
	void afterPropertiesSet() throws Exception;
}
```

但这并不是一个初始化Bean的完美方法，这种方法将Bean与容器绑定在了一起，替代的解决方案是通过配置文件配置"init-method"属性。

与`InitializingBean`类似，继承`org.springframeword.beans.factory.DisposableBean`接口，容器也会在Bean被销毁时调用其回调方法。

```java
package org.springframework.beans.factory;
public interface DisposableBean {
	void destroy() throws Exception;
}
```

下面是一个简单的示例：

```java
import org.springframework.beans.factory.DisposableBean;
import org.springframework.beans.factory.InitializingBean;
 
public class DemoBean implements InitializingBean, DisposableBean
{
    //Other bean attributes and methods
     
    @Override
    public void afterPropertiesSet() throws Exception
    {
        //Bean initialization code
    }
     
    @Override
    public void destroy() throws Exception
    {
        //Bean destruction code
    }
}
```

