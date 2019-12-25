## Spring Framework整体架构
![在这里插入图片描述](./resource/spring-framework-runtime.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3R6dzE5OTI=,size_16,color_FFFFFF,t_70)
## 核心容器
- **spring-core**：核心库，被多个其他模块引用。
- **spring-beans**：bean支持，包括Groovy。
- **spring-context**：运行时上下文，包括调度和远程调用抽象。
- **spring-context-indexer**：提供了索引功能，能在第一次扫描之后生成一个静态文件记录所有的组件，然后下一次扫描就直接读取文件中的内容，而不用再去执行扫描过程，从而提升启动运行速度。
- **spring-context-support**：包含用于集成第三方库到Spring上下文的类。
- **spring-expression**：Spring表达式语言（SpEL）。

## AOP和检测
- **spring-aop**：基于代理的AOP。
- **spring-aspects**：基于切面的AspectJ。
- **spring-instrument**：JVM引导的检测代理。

## 消息处理
- **spring-messaging**：消息处理的架构和协议。

## 数据访问与集成
- **spring-jdbc**：JDBC支持包，包括对数据源设置和JDBC访问支持。
- **spring-orm**：对象关系映射，包括对JPA和Hibernate支持。
- **spring-oxm**：对象XML映射。
- **spring-jms**：JMS支持包，包括发送和接收JMS消息的帮助类。
- **spring-tx**：事务基础，包括对DAO的支持及JCA的集成。

## Web
- **spring-web**：web支持包，包括客户端及web远程调用。
- **spring-webmvc**：REST web服务及web应用的MVC实现。
- **spring-websocket**：WebSocket和SockJS实现，包括对STOMP的支持。
- **spring-webflux**：响应式web框架，可以用来建立异步的、非阻塞的、事件驱动的服务。

## 日志
- **spring-jcl**：用于兼容不同版本的日志系统。

## 测试
- **spring-test**：单元测试和集成测试组件。
