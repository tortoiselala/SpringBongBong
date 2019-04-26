# 什么是Spring？

Spring是一个开源框架，Spring也就是Spring Framework。

来自wiki的定义：

>**Spring Framework**是一个开源的Java/Java EE全功能栈（full-stack）的应用程序框架。

来自"精通Spring4.x企业应用开发实战"的定义：

>Spring是分层的Java SE/EE 应用一站式轻量级开源框架，以IoC（Inverse of Control，控制反转）和AOP（Aspect Oriented Programming，切面编程）为内核，提供了展现层Spring MVC、持久层Spring JDBC及业务层事务管理等一站式的企业应用技术。Spring整合了许多第三方框架和类库，逐渐成为使用最多的请谅解JavaEE企业应用开源框架。

简单来说，Spring就是一个框架，能开发。ps：Spring4.x的很多术语都没有见过，要了解Spring还需要先了解以下，没有Spring之前，如何开发网站后台的，J2EE是干这个的。

# Spring体系结构

下图是Spring框架结构：

![](./image/spring_architecture.png)

<center>Spring框架结构</center>

## IoC

来自于"精通Spring4.x企业应用开发实战"的说明：

> Spring核心模块实现了Ioc的功能，它将类与类之间的依赖从代码中脱离出来，用配置的方式进行依赖关系描述，有IoC容器负责依赖类之间的创建、拼接、管理、获取等工作。BeanFactory接口是Spring框架的核心接口，它实现了容器许多核心的功能。

已经开始有点迷糊了，配置？容器？后面就明白了。

## AOP

来自"精通Spring4.x企业应用开发实战"的说明：

>AOP是继OOP之后，对编程设计思想影响极大的技术之一。AOP是进行横切逻辑编程的思想，它开拓了考虑问题的思路。

## 必备知识

### maven

mavem是一个项目构建与管理工具，构建过程中的几个注意的地方：

- GroupID 是项目组织唯一的标识符，实际对应JAVA的包的结构，是main目录里java的目录结构。 
- ArtifactID是项目的唯一的标识符，实际对应项目的名称，就是项目根目录的名称。

```xml
<groupId>com.yucong.commonmaven</groupId> 
<artifactId>commonmaven</artifactId> 
<version>0.0.1-SNAPSHOT</version> 
<packaging>jar</packaging> 
<name>common_maven</name> 
```

- groupId 定义了项目属于哪个组，举个例子，如果你的公司是mycom，有一个项目为myapp，那么groupId就应该是com.mycom.myapp. 
- artifacted 定义了当前maven项目在组中唯一的ID,比如，myapp-util,myapp-domain,myapp-web等。
- version 指定了myapp项目的当前版本，SNAPSHOT意为快照，说明该项目还处于开发中，是不稳定的版本。 
- name 声明了一个对于用户更为友好的项目名称，不是必须的，推荐为每个pom声明name，以方便信息交流。 

#### 什么是maven坐标

maven的世界中拥有数量非常巨大的构件，也就是平时用的一些jar,war等文件。 

maven定义了这样一组规则： 

世界上任何一个构件都可以使用Maven坐标唯一标志，maven坐标的元素包括groupId, artifactId, version，package，classifier。 

只要在pom.xml文件中配置好dependancy的groupId，artifact，verison，classifier, 

maven就会从仓库中寻找相应的构件供我们使用。那么，"maven是从哪里下载构件的呢？" 

答案很简单，maven内置了一个中央仓库的地址（http://repol.maven.org/maven2）,该中央仓库包含了世界上大部分流行的开源项目构件，maven会在需要的时候去那里下载。 

#### 坐标详解

```xml
<groupId>org.sonatype.nexus</groupId> 

<artifactId>nexus-indexer</artifactId> 

<version>2.0.0</version> 

<packaging>jar</packaging> 
```

- groupId 定义当前maven项目隶属的实际项目。 groupId的表示方式与Java包名的表示方式类似，如： 

```xml
<groupId>org.sonatype.nexus</groupId> 
```

- artifactId 该元素定义实际项目中的一个Maven项目（模块），推荐的做法是使用实际项目的名称作为artifactId的前缀。 如：

```xml
<artifactId>nexus-indexer</artifactId> 
```

在默认情况下，maven生成的构件，其文件名会以artifactId作为开头，如：nexus-indexer-2.0.0.jar。 packaging【可选的，默认为jar】： 

当不定义packaging时，maven会使用默认值jar。 

- classifier: 该元素用来帮助定义构件输出的一些附属构件。 项目构件的文件名是坐标相对应的，一般的规则为：artifact-version.packing

# Java web技术栈

## Java web基础资料

- 超全面 Java Web 视频教程[视频]
- Tomcat 与 Java Web 开发技术详解[书]

