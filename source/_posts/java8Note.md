title:  Java8笔记
description: 使用Java8时遇到的问题及解决方案
date: 2015-07-23
tags:  [Java8]
categories:  [Java8]

----------------------

1. <font color="red"> Java8 中引入  `default`   关键字，从而有了多继承问题，那么继承规则是什么？</font>
 基本上，你可以根据以下三条原则判断多继承的实现规则。
 * **类优先于接口**。 如果一个子类继承的父类和接口有相同的方法实现， 那么接口中的定义会被忽略。 这是为了让代码向后兼容。
 * **子类型中的方法优先于父类型中的方法**。 
 * 如果以上条件都不满足，则必须**显示覆盖/实现其方法**，或者声明成abstract。
 <!-- more -->
2. <font color="red"> Java8 的流操作可以使用 `peek` 来设置断点以调试、打印日志等</font>
 函数原型：`Stream<T> java.util.stream.Stream.peek(Consumer<? super T> action)`
 javadoc 描述如下：
 > Returns a stream consisting of the elements of this stream, additionally performing the provided action on each element as elements are consumed from the resulting stream.
 >  This is an intermediate operation. 
 >  For parallel stream pipelines, the action may be called at whatever time and in whatever thread the element is made available by the upstream operation. If the action modifies shared state, it is responsible for providing the required synchronization.
 
 调试：
 ```java
list.streams()
    .map(x->x * x)
    .peek(MyClass::forDebug) // 写成方法引用，可以在forDebug函数内部设置断点，forDebug简单返回参数就行
    .sum();

 ```
 打印日志：
  ```java
list.streams()
    .map(x->x * x)
    .peek(x -> log.info(x))  //打印日志，使用 println 打印
    .sum();

  ```

