---
title: SpringBoot 2.x | 第十一篇：初探 RabbitMQ 消息队列 
categories:
- SpringBoot
tags:
- SpringBoot

---



**MQ全称（Message Queue）又名消息队列，是一种异步通讯的中间件。**可以将它理解成邮局，发送者将消息传递到邮局，然后由邮局帮我们发送给具体的消息接收者（消费者），具体发送过程与时间我们无需关心，它也不会干扰我进行其它事情。**常见的MQ有kafka、activemq、zeromq、rabbitmq 等等，各大MQ的对比和优劣势可以自行Google**

[](#rabbitmq "rabbitmq")rabbitmq
================================

**RabbitMQ是一个遵循AMQP协议**，由面向高并发的`erlanng`语言开发而成，用在实时的对可靠性要求比较高的消息传递上，支持多种语言客户端。支持`延迟队列（这是一个非常有用的功能）`….

[](#基础概念 "基础概念")基础概念
--------------------

**Broker：**简单来说就是消息队列服务器实体  
**Exchange：**消息交换机，它指定消息按什么规则，路由到哪个队列  
**Queue：**消息队列载体，每个消息都会被投入到一个或多个队列  
**Binding：**绑定，它的作用就是把`exchange`和`queue`按照路由规则绑定起来  
**Routing Key：**路由关键字，`exchange`根据这个关键字进行消息投递  
**vhost：**虚拟主机，一个`broker`里可以开设多个`vhost`，用作不同用户的权限分离  
**producer：**消息生产者，就是投递消息的程序  
**consumer：**消息消费者，就是接受消息的程序  
**channel：**消息通道，在客户端的每个连接里，可建立多个`channel`，每个`channel`代表一个会话任务



[](#常见应用场景 "常见应用场景")常见应用场景
--------------------------

1.  邮箱发送：用户注册后投递消息到`rabbitmq`中，由消息的消费方异步的发送邮件，提升系统响应速度
2.  流量削峰：一般在秒杀活动中应用广泛，秒杀会因为流量过大，导致应用挂掉，为了解决这个问题，一般在应用前端加入消息队列。用于控制活动人数，将超过此一定阀值的订单直接丢弃。缓解短时间的高流量压垮应用。
3.  订单超时：利用`rabbitmq`的延迟队列，可以很简单的实现**订单超时**的功能，比如用户在下单后30分钟未支付取消订单
4.  还有更多应用场景就不一一列举了…..

[](#导入依赖 "导入依赖")导入依赖
====================

在 `pom.xml` 中添加 `spring-boot-starter-amqp`的依赖

    <dependencies>  
     <dependency>  
     <groupId>org.springframework.boot</groupId>  
     <artifactId>spring-boot-starter-amqp</artifactId>  
     </dependency>  
     <dependency>  
     <groupId>com.alibaba</groupId>  
     <artifactId>fastjson</artifactId>  
     <version>1.2.46</version>  
     </dependency>  
     <dependency>  
     <groupId>org.springframework.boot</groupId>  
     <artifactId>spring-boot-starter-web</artifactId>  
     </dependency>  
     <dependency>  
     <groupId>org.springframework.boot</groupId>  
     <artifactId>spring-boot-starter-test</artifactId>  
     <scope>test</scope>  
     </dependency>  
    </dependencies>  

[](#属性配置 "属性配置")属性配置
====================

在 `application.properties` 文件中配置`rabbitmq`相关内容，值得注意的是这里配置了手动ACK的开关

    spring.rabbitmq.username=battcn  
    spring.rabbitmq.password=battcn  
    spring.rabbitmq.host=192.168.0.133  
    spring.rabbitmq.port=5672  
    spring.rabbitmq.virtual-host=/  
    \# 手动ACK 不开启自动ACK模式,目的是防止报错后未正确处理消息丢失 默认 为 none  
    spring.rabbitmq.listener.simple.acknowledge-mode=manual  

[](#具体编码 "具体编码")具体编码
====================

[](#定义队列 "定义队列")定义队列
--------------------

如果手动创建过或者`RabbitMQ`中已经存在该队列那么也可以省略下述代码…

    package com.battcn.config;  
      
    import org.springframework.amqp.core.Queue;  
    import org.springframework.context.annotation.Bean;  
    import org.springframework.context.annotation.Configuration;  
      
    /**  
     * RabbitMQ配置  
     *  
     * @author Levin  
     * @since 2018/4/11 0011  
     */  
    @Configuration  
    public class RabbitConfig {  
      
     public static final String DEFAULT\_BOOK\_QUEUE = "dev.book.register.default.queue";  
     public static final String MANUAL\_BOOK\_QUEUE = "dev.book.register.manual.queue";  
      
     @Bean  
     public Queue defaultBookQueue() {  
     // 第一个是 QUEUE 的名字,第二个是消息是否需要持久化处理  
     return new Queue(DEFAULT\_BOOK\_QUEUE, true);  
     }  
      
     @Bean  
     public Queue manualBookQueue() {  
     // 第一个是 QUEUE 的名字,第二个是消息是否需要持久化处理  
     return new Queue(MANUAL\_BOOK\_QUEUE, true);  
     }  
    }  

[](#实体类 "实体类")实体类
-----------------

创建一个`Book`类

    public class Book implements java.io.Serializable {  
      
     private static final long serialVersionUID = -2164058270260403154L;  
      
     private String id;  
     private String name;  
     // 省略get set ...  
    }  

[](#控制器 "控制器")控制器
-----------------

编写一个`Controller`类，用于消息发送工作

    package com.battcn.controller;  
      
    import com.battcn.config.RabbitConfig;  
    import com.battcn.entity.Book;  
    import com.battcn.handler.BookHandler;  
    import org.springframework.amqp.rabbit.core.RabbitTemplate;  
    import org.springframework.beans.factory.annotation.Autowired;  
    import org.springframework.web.bind.annotation.GetMapping;  
    import org.springframework.web.bind.annotation.RequestMapping;  
    import org.springframework.web.bind.annotation.RestController;  
      
    /**  
     * @author Levin  
     * @since 2018/4/2 0002  
     */  
    @RestController  
    @RequestMapping(value = "/books")  
    public class BookController {  
      
     private final RabbitTemplate rabbitTemplate;  
      
     @Autowired  
     public BookController(RabbitTemplate rabbitTemplate) {  
     this.rabbitTemplate = rabbitTemplate;  
     }  
      
     /**  
     * this.rabbitTemplate.convertAndSend(RabbitConfig.DEFAULT\_BOOK\_QUEUE, book); 对应 {@link BookHandler#listenerAutoAck}  
     * this.rabbitTemplate.convertAndSend(RabbitConfig.MANUAL\_BOOK\_QUEUE, book); 对应 {@link BookHandler#listenerManualAck}  
     */  
     @GetMapping  
     public void defaultMessage() {  
     Book book = new Book();  
     book.setId("1");  
     book.setName("一起来学Spring Boot");  
     this.rabbitTemplate.convertAndSend(RabbitConfig.DEFAULT\_BOOK\_QUEUE, book);  
     this.rabbitTemplate.convertAndSend(RabbitConfig.MANUAL\_BOOK\_QUEUE, book);  
     }  
    }  

[](#消息消费者 "消息消费者")消息消费者
-----------------------

默认情况下 `spring-boot-data-amqp` 是自动`ACK`机制，就意味着 MQ 会在消息消费完毕后自动帮我们去ACK，这样依赖就存在这样一个问题：**如果报错了，消息不会丢失，会无限循环消费，很容易就吧磁盘空间耗完，虽然可以配置消费的次数但这种做法也有失优雅。目前比较推荐的就是我们手动ACK然后将消费错误的消息转移到其它的消息队列中，做补偿处理**

    package com.battcn.handler;  
      
    import com.battcn.config.RabbitConfig;  
    import com.battcn.entity.Book;  
    import com.rabbitmq.client.Channel;  
    import org.slf4j.Logger;  
    import org.slf4j.LoggerFactory;  
    import org.springframework.amqp.core.Message;  
    import org.springframework.amqp.rabbit.annotation.RabbitListener;  
    import org.springframework.stereotype.Component;  
      
    import java.io.IOException;  
      
    /**  
     * BOOK_QUEUE 消费者  
     *  
     * @author Levin  
     * @since 2018/4/11 0011  
     */  
    @Component  
    public class BookHandler {  
      
     private static final Logger log = LoggerFactory.getLogger(BookHandler.class);  
      
     /**  
     * <p>TODO 该方案是 spring-boot-data-amqp 默认的方式,不太推荐。具体推荐使用  listenerManualAck()</p>  
     * 默认情况下,如果没有配置手动ACK, 那么Spring Data AMQP 会在消息消费完毕后自动帮我们去ACK  
     * 存在问题：如果报错了,消息不会丢失,但是会无限循环消费,一直报错,如果开启了错误日志很容易就吧磁盘空间耗完  
     * 解决方案：手动ACK,或者try-catch 然后在 catch 里面讲错误的消息转移到其它的系列中去  
     * spring.rabbitmq.listener.simple.acknowledge-mode=manual  
     * <p>  
     *  
     * @param book 监听的内容  
     */  
     @RabbitListener(queues = {RabbitConfig.DEFAULT\_BOOK\_QUEUE})  
     public void listenerAutoAck(Book book, Message message, Channel channel) {  
     // TODO 如果手动ACK,消息会被监听消费,但是消息在队列中依旧存在,如果 未配置 acknowledge-mode 默认是会在消费完毕后自动ACK掉  
     final long deliveryTag = message.getMessageProperties().getDeliveryTag();  
     try {  
     log.info("[listenerAutoAck 监听的消息] - [{}]", book.toString());  
     // TODO 通知 MQ 消息已被成功消费,可以ACK了  
     channel.basicAck(deliveryTag, false);  
     } catch (IOException e) {  
     try {  
     // TODO 处理失败,重新压入MQ  
     channel.basicRecover();  
     } catch (IOException e1) {  
     e1.printStackTrace();  
     }  
     }  
     }  
      
     @RabbitListener(queues = {RabbitConfig.MANUAL\_BOOK\_QUEUE})  
     public void listenerManualAck(Book book, Message message, Channel channel) {  
     log.info("[listenerManualAck 监听的消息] - [{}]", book.toString());  
     try {  
     // TODO 通知 MQ 消息已被成功消费,可以ACK了  
     channel.basicAck(message.getMessageProperties().getDeliveryTag(), false);  
     } catch (IOException e) {  
     // TODO 如果报错了,那么我们可以进行容错处理,比如转移当前消息进入其它队列  
     }  
     }  
    }  

[](#主函数 "主函数")主函数
-----------------

    package com.battcn;  
      
    import org.springframework.boot.SpringApplication;  
    import org.springframework.boot.autoconfigure.SpringBootApplication;  
      
    /**  
     * @author Levin  
     */  
    @SpringBootApplication  
    public class Chapter11Application {  
      
     public static void main(String[] args) {  
     SpringApplication.run(Chapter11Application.class, args);  
     }  
    }  

[](#测试 "测试")测试
--------------

完成准备事项后，启动`Chapter11Application` 访问 [http://localhost:8080/books](http://localhost:8080/books) 将会看到如下内容，就代表一切正常….

    2018-05-22 19:04:26.708  INFO 23752 --- [cTaskExecutor-1] com.battcn.handler.BookHandler           : [listenerAutoAck 监听的消息] - [com.battcn.entity.Book@77d8be18]  
    2018-05-22 19:04:26.709  INFO 23752 --- [cTaskExecutor-1] com.battcn.handler.BookHandler           : [listenerManualAck 监听的消息] - [com.battcn.entity.Book@8bb452]  