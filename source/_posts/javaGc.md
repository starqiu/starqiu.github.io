title: java垃圾回收机制笔记
description: 深入理解Java垃圾回收机制（目的、算法及执行机制）
date: 2015-07-22
mathjax: true
tags:  [Java , GC]
categories:  [Java , GC]
------

## 目的
　垃圾回收可以有效的防止内存泄露，有效的使用空闲的内存。
## 算法
### 引用计数法(Reference Counting Collector)
- 被引用则计数加１，不再引用则减１。为０则标为垃圾，可被回收。
- **<font color ="red">很快，但无法检测出循环引用。</font>**

### 标记-清除算法(mark and sweep)
- 标记：　把所有的引用关系看作一张图，从一个节点GC ROOT开始，寻找对应的引用节点，找到这个节点以后，继续寻找这个节点的引用节点，当所有的引用节点寻找完毕之后，剩余的节点则被认为是没有被引用到的节点，即无用的节点。
- 清除：　直接回收无用的节点**<font color ="red">（会造成内存碎片）</font>**
- java中可作为GC Root的对象有　【虚拟机栈中引用的对象（本地变量表），　方法区中静态属性引用的对象，方法区中常量引用的对象，本地方法栈中引用的对象（Native对象）】

### 标记-整理算法(mark and compact)
- 在标记－清除算法的基础上，将存活对象往空闲空间移动
- 一般增加句柄和句柄表, **<font color ="red">解决了内存碎片问题，但成本更高</font>**

### 复制算法(Compacting Collector)
- 开始时把堆分成 一个对象 面和多个空闲面， 程序从对象面为对象分配空间，当对象满了，基于copying算法的垃圾收集就从根集中扫描活动对象，并将每个 活动对象复制到空闲面(使得活动对象所占的内存之间没有空闲洞)，这样空闲面变成了对象面，原来的对象面变成了空闲面，程序会在新的对象面中分配内存。
- 一种典型的基于coping算法的垃圾回收是stop-and-copy算法，它将堆分成对象面和空闲区域面，在对象面与空闲区域面的切换过程中，程序暂停执行。
- **<font color ="red">克服句柄的开销 , 解决堆碎片</font>**

### generation算法(Generational Collector)
<center>![Generational Collector](/images/GenerationalCollector.jpg) </center>
<!-- more -->
 - 分代的垃圾回收策略，是基于这样一个事实：<font color= "red">**不同的对象的生命周期是不一样的**</font>。因此，不同生命周期的对象可以采取不同的回收算法，以便提高回收效率。
 - 年轻代（Young Generation）
    * 所有新生成的对象首先都是放在年轻代的。年轻代的目标就是尽可能快速的收集掉那些生命周期短的对象。
    * **<font color ="red">新生代内存按照8:1:1的比例分为一个eden区和两个survivor(survivor0,survivor1)区</font>**。一个Eden区，两个 Survivor区(一般而言)。
    * 大部分对象在Eden区中生成。回收时先将eden区存活对象复制到一个survivor0区，然后清空eden区，当这个survivor0区也存放满了时，则将eden区和survivor0区存活对象复制到另一个survivor1区，然后清空eden和这个survivor0区，此时survivor0区是空的，然后将survivor0区和survivor1区交换，即保持survivor1区为空， 如此往复。
    * 当survivor1区不足以存放 eden和survivor0的存活对象时，就将存活对象直接存放到老年代。若是老年代也满了就会触发一次Full GC，也就是新生代、老年代都进行回收
    * 新生代发生的GC也叫做Minor GC，MinorGC发生频率比较高(不一定等Eden区满了才触发)
 - 年老代（Old Generation）
    *  在年轻代中经历了N次垃圾回收后仍然存活的对象，就会被放到年老代中。因此，可以认为年老代中存放的都是一些生命周期较长的对象。
    *  **<font color ="red">内存比新生代也大很多(大概比例是1:2)</font>**，当老年代内存满时触发Major GC即 Full GC，Full GC发生频率比较低，老年代对象存活时间比较长，存活率标记高。
 - 持久代（Permanent Generation）
 用于存放静态文件，如Java类、方法等。持久代对垃圾回收没有显著影响，但是有些应用可能动态生成或者调用一些class，例如Hibernate 等，在这种时候需要设置一个比较大的持久代空间来存放这些运行过程中新增的类。

##  垃圾收集器
 * 新生代收集器使用的收集器：Serial、PraNew、Parallel Scavenge
 * 老年代收集器使用的收集器：Serial Old、Parallel Old、CMS
 * Serial收集器（复制算法): 新生代单线程收集器，标记和清理都是单线程，优点是简单高效。
 * Serial Old收集器(标记-整理算法): 老年代单线程收集器，Serial收集器的老年代版本。
 * ParNew收集器(停止-复制算法): 新生代收集器，可以认为是Serial收集器的多线程版本,在多核CPU环境下有着比Serial更好的表现。
 * Parallel Scavenge收集器(停止-复制算法): 并行收集器，追求高吞吐量，高效利用CPU。吞吐量一般为99%， 吞吐量= 用户线程时间/(用户线程时间+GC线程时间)。适合后台应用等对交互相应要求不高的场景。
 * Parallel Old收集器(停止-复制算法): Parallel Scavenge收集器的老年代版本，并行收集器，吞吐量优先
 * CMS(Concurrent Mark Sweep)收集器（标记-清理算法）: 高并发、低停顿，追求最短GC回收停顿时间，cpu占用比较高，响应时间快，停顿时间短，多核cpu 追求高响应时间的选择

##  执行机制
### Scavenge GC 
 一般情况下，当新对象生成，并且在Eden申请空间失败时，就会触发Scavenge GC，对Eden区域进行GC　**<font color ="red">（频繁进行，　使用速度快、效率高的算法）</font>**
### Full GC 
 对整个堆进行整理，包括Young、Tenured和Perm。**<font color ="red">(速度慢,调优集中点)</font>**
##  内存泄露
 * 静态集合类像HashMap、Vector等的使用最容易出现内存泄露，这些静态变量的生命周期和应用程序一致，所有的对象Object也不能被释放，因为他们也将一直被Vector等应用着。
 * 各种连接，数据库连接，网络连接，IO连接等没有显示调用close关闭，不被GC回收导致内存泄露。
 * 监听器的使用，在释放对象的同时没有相应删除监听器的时候也可能导致内存泄露。

## 参考文献　
[1] : 　[深入理解java垃圾回收机制](http://www.cnblogs.com/sunniest/p/4575144.html)