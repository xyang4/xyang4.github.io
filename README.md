# xyang4.github.io
智联某互联网公司高级Java开发招聘需求：

- 深入理解 JAVA 集合，多线程编程等相关基础知识和 JVM 原理；                          java基础、多线程、JVM
- 熟练使用 SQL 语句及优化，对数据库事务、锁、索引有深入理解；                    数据库优化
- 熟悉 Spring Boot、Spring Cloud 及微服务周边中间件，有实践经验；		      微服务相关
- 熟悉常见数据结构和算法及设计模式，有分布式系统设计经验；			              数据结构、设计模式及算法
- 深入理解常用的缓存中间件如 redis，memcache，具备分布式缓存设计经验；缓存及使用经验
- 具备良好的编码规范和软件工程思维；	           编码习惯、OOP及解决问题的思维、方式方法
- 有 Hadoop 大数据开发经验者优先                 	大数据相关：Spark、Hadoop（最好是能说明白 Yarn 调度原理）
- 具备独立分析和解决问题能力，积极主动、认真踏实，有良好的协调沟通能力。     



---



第一章 Core Java

1. Java 基础及集合

- String 为什么是 Final 的（高率、安全）？
- 简单描述下OO的特性（封装、继承、多态）
- 接口与抽象类的区别
- 反射的用途及实现
- HashMap( 初始容量是2的指数幂、加载因子0.75、扩容死锁机环链形行程分析 、链表转红黑树)
- HashSet、ArrayList、ConcurrentHashMap 实现原理
- java spi 动态服务扩展机制

Service Provider Interface，应用于厂商自定义组件或插件中，为某个接口寻找服务实现的机制。

- 类加载机制

类加载器

    启动（Bootstrap）类加载器  	负责将 Java_Home/lib 下面的类库加载到内存中（比如 rt.jar）。	由于引导类加载器涉及到虚拟机本地实现细节，开发者无法直接获取到启动类加载器的引用，所以不允许直接通过引用进行操作。
   标准扩展（Extension）类加载器 	它负责将 Java_Home /lib/ext 或者由系统变量 java.ext.dir 指定位置中的类库加载到内存中。	开发者可以直接使用标准扩展类加载器。                      
  应用程序（Application）类加载器	它负责将系统类路径（CLASSPATH）中指定的类库加载到内存中。       	开发者可以直接使用系统类加载器。由于这个类加载器是 ClassLoader 中的 getSystemClassLoader() 方法的返回值，因此一般称为系统（System）加载器。



- 双亲委派模型

除了顶层的启动类加载器外，其余的类加载器都应该有自己的父类加载器，而这种父子关系一般通过组合（Composition）关系来实现，而不是通过继承（Inheritance）.

委派过程

		某个特定的类加载器在接到加载类的请求时，首先将加载任务委托给父类加载器，依次递归，如果父类加载器可以完成类加载任务，就成功返回；只有父类加载器无法完成此加载任务时，才自己去加载。

系统实现

		在 java.lang.ClassLoader 的 loadClass() 方法中，先检查是否已经被加载过，若没有加载则调用父类加载器的 loadClass() 方法，若父加载器为空则默认使用启动类加载器作为父加载器。如果父加载失败，则抛出 ClassNotFoundException 异常后，再调用自己的 findClass() 方法进行加载。

- 线程上下文类加载器
- 深拷贝与浅拷贝的区别？

  浅拷贝 	                                        	不复制堆内存中的对象
  深拷贝 	复制基本类型的属性；引用类型的属性复制，复制栈中的变量 和 变量指向堆内存中的对象的指针	复制堆内存中的对象 

- BIO、NIO、AIO 有什么区别？
- 内存泄漏与内存溢出的区别

2. Web相关

- 为什么Http 三次握手四次分手
- Session 分布式处理方案及其原理
- JDBC 流程
- MVC 设计思想
- 同步和异步，阻塞和非阻塞。
- OSI七层模型

3. 算法及数据结构

- 排序

4. JVM 相关

- 垃圾回收
- Jvm 调优

5. 异常体系

- 常见的异常

---

第二章 框架

1 Spring

- Spring mvc
- Bean 的生命周期
- Spring Ioc
- 

2 Mybatis

- 简述其运行原理
- 用到的设计模式
  - Builder 模式：SqlSessionFactoryBuilder、XMLConfigBuilder、XMLMapperBuilder、XMLStatementBuilder、CacheBuilder
  - 工厂模式 ：SqlSessionFactory、ObjectFactory、MapperProxyFactory等
  - 单例模式：ErrorContext和LogFactory；
  - 代理模式：Mybatis实现的核心，比如MapperProxy、ConnectionLogger，用的jdk的动态代理；还有executor.loader包使用了cglib或者javassist达到延迟加载的效果；
  - 适配器模式：例如Log的Mybatis接口和它对jdbc、log4j等各种日志框架的适配实现；

3 全文检索

3.1 基本原理

- 倒排索引

3.2 组件

- Lucene
- ES

4 Dubbo

第三章 数据库

1 Mysql

基础

- 运行原理
- 索引：Innodb引擎原理、索引的本质及原理
- 红黑树、B树，B+树原理
- 行锁，表锁；乐观锁，悲观锁
- 数据库事务的集中粒度

常见问题

- sql 优化方案
- 聚簇索引与非聚簇索引的区别

2 Nosql

Redis

- redis 内部结构

- Redis 为什么是单线程的

- Redis 内存淘汰机制、持久化机制

MongoDb (非必须)

第四章 高并发

1 并发基础

- 线程生命周期、运行及执行原理
- 线程池运行原理

2 锁机制

- volatile、synchronized 关键字实现原理
- CAS、ABA问题

---

第五章 项目实战

1 架构演变

单体项目 -> 集群部署 -> 服务拆分 -> 微服务





2  微服务

微服务基础

Spring Boot

- 说说你的理解
- 自动装配的原理

Spring Cloud

Spring Boot + Dubbo + Nexus

核心技术

- 分布式锁
- 分布式主键
- 分布式事务
- Mysql 分库分表

3 缓存

- 缓存的合理性
- 缓存崩溃、缓存降级



4 消息队列

基本原理及常用模型

- 消息重发补偿、幂等性及消息堆积的解决思路
- 如何保证消息的有序性



5 常用中间件

RabbitMq

Kafka

- 基本原理

Zookeeper

- 基本原理
- 选举算法
- 假死脑裂：

该问题就是服务集群因为网络震荡导致的多主多从问题，解决方案就是设置服务切换的超时时间，但也同时会导致无法达到高可用的要求





5 设计模式

懂了设计模式就懂了面向对象的分析方法和设计（OOA/D）的精要.

七大原则

- 单一职责
- 接口隔离
- 依赖倒转（倒置）
- 里氏替换
- 开闭原则
- 迪米特法则
- 合成复用



