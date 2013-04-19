---
author: Bear
comments: true
date: 2013-01-14 11:54:01
layout: post
slug: java-nio-brief
title: Java NIO 简要
wordpress_id: 97
categories:
- 技术流/TechGangster
tags:
- nio
---

来源于Java 1.4的java.nio软件包，被命名为New I/O，随着时间流逝，已经不算New了，称为Non-Blocking I/O还是更合适一些。

Java nio的三个核心：



	
  * Buffer

	
  * Channel

	
  * Selector


Buffer包装了基本数据元素数组对象，处理数据缓存，作为一个缓冲区，是nio数据读或写的中转地。

Channel提供了操作文件描述方法，实现类调用底层操作系统低级IO方法read，write，处理Buffer对象读写，是Buffer对象的唯一接口。是数据的源头或者数据的目的地。
![Buffer&Channel](http://ww2.sinaimg.cn/mw690/6fbda5afgw1e0sy54f9d8j.jpg)
Buffer与Channel提高了I\O效率，Buffer以数据块代替了字节传输数据，而Channel作为双向通道，同时能检查Buffer块是否准备完毕，如果没有则返回执行其他任务等待下次轮询或者通知，而不阻塞在此等待数据，这就是非阻塞I\O。

但NIO真正厉害的，精髓所在是第三个核心，Selector。有了Selector，将SocketChannel注册到Selector上，并标明SelectorKey关注的是哪类数据操作(读，写，建立连接，接受连接等)。Selector筛选准备好的Socket，提供给工作线程进行逻辑加工响应请求，这就可以将NIO衍生到Web服务的解决方案，即是NIO的卖点：I/O multiplexing(IO多路复用) + Non-blocking I/O(非阻塞IO)。

Selector用到的设计模式是Reactor模式。Reactor模式翻译为反映堆模式还是准确的。Reactor模式是对多个同步事件进行分拣和派发。做一个比喻就是，一个人去钓鱼，撑出了好多支的鱼竿，然后就一边和旁边的MM聊天，一边观察这一排的鱼竿有没有鱼上钩的，如果其中有鱼竿有动作，那么就把鱼钓上来。在这里，鱼相当于数据或者请求，鱼竿代表Socket Channel，而人，就是Selector。这个组成就是一个典型的Reactor模式。这个比喻也是现在以NIO为基础的服务器的大致结构。
![Old IO & New IO](http://ww1.sinaimg.cn/mw690/6fbda5afgw1e0sy54sx1dj.jpg)
传统的服务器，如Jboss，有多少个请求连接，就创建多少线程，分别处理请求，当请求连接遇到网络问题时，则线程阻塞等待。在高并发的情况下，由于阻塞造成大量请求堆积，以及频繁的线程上下文的切换占用资源，对于服务器来说都是致命的。
<!-- more -->
如果换成NIO模式的处理请求，则是由一个线程统一管理所有进来的连接，这个线程持有的Selector对连接进行轮询，整理出已经准备完毕的连接，并派发给工作线程，让工作线程处理请求所想要的逻辑并响应结束掉这个连接，以便工作线程重复使用，接入下一个请求。将接收请求和处理请求两个阶段解藕，管理请求的前台线程和处理请求的后台线程分工合作，让服务器的资源得到合理使用。Tomcat是支持NIO的服务器，而Jetty则是支持NIO的Servlet容器。而Netty，Mina，Grizzly等都是以NIO原理为基础的框架，能依场景需求做出定制化的服务器端满足需求。

综上所述，NIO带来了：



	
  * 避免不必要的多线程(处理请求线程<连接数)

	
  * 单线程处理多任务(接收请求线程一夫当关万夫莫敌)

	
  * 非阻塞IO(线程处理IO阻塞来去自由)

        
  * IO多路复用(本次阻塞也没关系，可等下次又轮询到时操作I\O)

        
  * 基于块传输，比流传输更高效(正常情况)



但同时，使用NIO并不一定带来高性能，下述4个场景是根据大牛经验总结的不合适场景

	
  * 客户端应用

	
  * 连接数<1000

	
  * 并发程度不高

	
  * 局域网环境下


最后对于我们是否需要利用NIO框架自己搭建服务，可以套用国外网友回答"到底是用Netty还是Jetty"的问题：

Jetty has had support for asynchronous request processing since version 6, using a proprietary API. More recent versions support the asynchronous API as part of the Servlet 3.0 API, like any other compliant implementation.

Using Netty would seem like a lot of work for little gain, unless you have highly specific requirements. Otherwise, Jetty would do the job for you with minimal effort.

若有高度定制化需求，则采用NIO框架自己搭建，若没有，则采用已经存在的服务器，避免重复制造轮子的过程。我暂时看不出来我们的应用有能够高度定制的地方，并且作为前端应用，搭建出符合安全，细节，以及能与原体系架构能匹配的服务器，需要花费很大的功夫，但对于性能有多少提升，并不明朗。

-----------------

既然说到NIO，再搭车说说其他几种IO。
![4 kinds of io](http://ww3.sinaimg.cn/mw690/6fbda5afgw1e0t0mnlztoj.jpg)
看图说话，非阻塞，阻塞IO都属于同步IO，异步IO的效率远远高于同步IO。
点击[这里](http://blog.csdn.net/historyasamirror/article/details/5778378)，这篇文很好的解释了这4个概念。我就不重复说了，这个知识还是很重要的。

