---
author: Bear
comments: true
date: 2013-03-12 16:37:53
layout: post
slug: java-concurrency-in-practice-part-ii-structuring-concurrent-applications
title: Java并发编程笔记-PART II.构建并发应用
wordpress_id: 120
categories:
- 笔记
tags:
- concurrency
- Java并发编程
---

第一部分讲完了并发的一些基础原理，接着开始讲具体怎样构建并发程序。

Chapter 6. Task Execution

用多线程代替单个主线程，将任务派发给多个线程执行。带来三个影响点：

   * 处理任务的工作从主线程脱离出来，使得主线程能更快处理下一个进来的请求。提高响应速度。
   * 任务被平行的处理，对多个请求能同时提供服务，在多核处理器或者任务被阻塞时(如IO，锁，资源等待)，会提高性能。
   * 任务处理代码必须线程安全，因为可能会并发的被多任务引用。

如果创建线程无穷无尽，肯定会出现问题，系统资源吃紧。首先创建和销毁线程都需要额外的cpu和内存资源，其次由于cpu核数有效，过多的线程会因为分配时间片的间隔过久导致闲置状态过久，同样消耗内存。第三，会对系统的稳定性造成影响，太多的线程可能会导致OutOfMemoryError，及其冒险。开多少线程能让应用保持最佳的效率性能，是需要评测对比性能测试数据调试到最佳状态。
<!-- more -->
顺序执行任务的瓶颈是低效的响应和吞吐量，多线程执行任务的瓶颈是资源管理。
Executor提供了将任务提交从任务执行解藕出来的标准方法，用Runnable描述任务，Executor的实现类提供了生命周期控制，监控等一系列任务管理功能。
Executor是基于生产者-消费者模式的，提交任务的是生产者，线程执行任务则是消费者，用Executor通常是最简单的途径来实现生产者-消费者模式的设计。
任务执行策略有以下几点：

   * 任务在哪个线程被执行?
   * 任务执行顺序是怎样的(FIFO,LIFO,priority order)?
   * 多少任务能同时执行?
   * 多少任务必须排队执行？
   * 当因为系统过载而拒绝一个任务时，拒绝哪个任务，并能被系统知晓?
   * 在执行任务前后还需要做哪些动作?

执行策略是一种资源管理工具，最理想的策略依靠可用的计算资源以及服务质量的需求。

上面说到线程对应任务无限制会对系统资源造成压力压垮系统，所以产生了线程池这个概念。线程池管理着一池相同的工作线程。通常线程池和任务等待队列亲密无间。工作线程的生命简单:从工作队列中请求下一个任务，执行它，再回线程池等待另一个任务。
用线程池的好处有很多，比如复用已经存在的线程，这样就不需要反复创建和销毁线程。通过调整线程池的大小，能充分的利用cpu，让其处于饱和状态，又恰到好处的不至于让你的应用出现OutOfMemory，或者线程间竞争资源过于激烈。类库提供了多种线程池，newFixedThreadPool , newCachedThreadPool ，newSingleThreadExecutor，newScheduledThreadPool，各有其特征，在此不多写。
用线程池代替线程对应任务的优势是提高了系统的稳定性，不会再创造成百上千的线程挤垮cpu和内存，并实现了优雅降级的限流。

Executor的生命周期控制关系到JVM。如果线程没有终止，那么JVM也不会终止。生命周期基本有三个状态:running，shutting down，terminated。对于生命周期的控制，能做到优雅关闭，即等待开始的任务完成同时拒绝提交新任务，也可直接关闭所有任务。

从某些方面来说，在处理延时以及周期性的任务上，ScheduledThreadPoolExecutor比Timer有优势。例如Timer是单线程的，处理时间任务可能会导致拖延以及分配不均。但是TimerTask则是多线程同时进行避免了任务等待。另外，如果Timer遇到异常，则很可能不不捕获，导致整个进程就取消影响所有任务。TimerTask则会遇到线程泄漏这个问题，后面章节再聊。

Chapter 7.  Cancellation and Shutdown

以前都是说开始容易结束难，现在也有说难的不是结束而是怎么开始。总之都有道理了。在Java进程里终止线程还是比较绕的事情。Thread.stop()是被废弃的方法，原因是其非常的不安全不礼貌。替代办法是用中断(Interruption)，是一种合作机制让线程告
诉其他线程停止现在所在做的事情。

取消任务的原因很多，比如用户请求取消，时间限制取消，应用事件取消，错误，关闭。

中断机制是实现取消行为最明智的方法。调用Interrupt方法不会强制线程终止所在做的事情，而是传递需要中断的请求，改变isInterrupted的状态。线程能在下一次更合适停止的时候停止。有些方法，例如sleep，join，wait，会抛出InterruptException以及改变中断状态。

响应中断方式两种，1)传播它，让你的方法是中断阻塞式的。method() throws InterruptedException {} .2)用变量存储状态，传递给更高一级的代码层。在清楚某线程中断策略后方可使用中断。

第7章看得好累，不想多写跳第下章去了。Java没有提供抢占机制来结束多线程，而是以协作机制来替代，利用FurtureTask和Executor框架能比较方便的取消任务和服务。

Chapter 8. Applying Thread Pools

任务类型和执行策略有潜在的耦合。任务特性需求的执行策略大致分几种：任务依赖型，任务受限线程型，响应时间敏感型，用ThreadLocal的任务。

线程池应用在任务类型一致以及独立的情况下效果最好。有死锁限制的任务相互依赖，最好用无界的线程池，否则可能会卡死。长时间执行的任务也会把线程池弄的阻塞，需要设置时间限制。

线程池开多大合适?如果是纯计算偏向的，线程数设置为Ncpu+1就可以了，所有cpu都在工作以及多加一个防止一些缺页中断发生时替补进去不浪费时间。但是对于有I/O操作以及阻塞的任务，就需要更多线程来提高效率。公式如下:
Nthreads = Ncpu * Ucpu * ( 1 + W/C )
Ucpu 代表想要的cpu使用率介于0%~100%
W是cpu等待时间，C是cpu计算时间
当然这也只是一个推算与CPU相关的，还有与网络，数据库，内存等相关资源也会影响到计算。例如线程池大于连接池，那么连接池就是瓶颈，反之，则是线程池是瓶颈。

线程池执行器的构造函数参数如下:
public ThreadPoolExecutor( 
             int corePoolSize, 
             int maximumPoolSize,
             long keepAliveTime,
             TimeUnit unit,
             BlockingQueue workQueue)
corePoolSize是保留的线程数，maximumPoolSize是线程池最大数，keepAliveTime以及unit分别表示存活时间以及时间单位，workQueue表示的是存放任务的队列。

任务队列有三种，有界队列(bounded Queue)，无界队列(unbounded Queue)以及同步队列(synchronous Queue)。有界队列对于资源控制很有帮助，网络服务基本都用有界防止攻击，但在任务有互相依赖的情况下容易造成死锁。无界队列很好，但过大的负载会对环境造成压力挂掉。同步队列不算真正的队列，在有空余线程时，才放入一个任务让线程执行，否则执行饱和策略。

任务队列装满了以后，多余的任务怎么办，这时候用到饱和策略(Saturation Policies)。在ThreadPoolExecutor中setRejectedExecutionHandler()设置。常用的几种模式，中止抛出异常(AbortPolicy), 主线程执行(CallerRunsPolicy), 安静忽略(DiscardPolicy), 扔掉将要执行的任务，提交新任务(DiscardOldestPolicy)。

Executor是强大灵活应用于并发任务执行的框架。提供了很多调整选项，比如创造销毁线程的策略，处理任务队列以及处理任务的策略。虽然是最强大的框架，但一些设置的组合重叠效果会不佳，比如特殊的任务需要特殊的执行策略，一些参数的组合会导致产生奇怪的结果。

Chapter 9.GUI Applications 跳过，我和图形界面暂时没有什么缘分。

2/4 to be continue.
