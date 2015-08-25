title:  Java笔记
description: 使用Java时遇到的问题及解决方案
date: 2015-07-21
tags:  [Java]
categories:  [Java]

----------------------

1. <font color="red">静态导入（Static Import）</font>
 一般情况下，我们调用余弦的方式如下：
 ```java
    double r = Math.cos(Math.PI * theta);
 ```
 即在前面加入引用类 `Math` , 当我们经常使用这个函数时就会显得不厌其烦。一种解决方案是静态导入。
 使用
 ```java
 import static java.lang.Math.PI;
 import static java.lang.Math.cos;
 ```
 或
 ```java
 import static java.lang.Math.*;
 ```
 则可以这样调用：
 ```java
double r = cos(PI * theta);
 ```
 需要注意的是：<font color=red>并不推荐这样做</font>。只有当一个方法或是变量经常使用时才使用静态导入，不然很容易造成误解，以为 `cos` 方法是当前类的方法，可读性差。个人比较喜欢在测试用例或是非产品类的项目中使用静态导入。
  参考: <http://docs.oracle.com/javase/1.5.0/docs/guide/language/static-import.html>

2. <font color="red">接口都继承自Object吗？如果不是，那为什么接口有equals方法？</font>
 ```
public class Test {
    public static void main(String[] args) {
        Employee e = null;
        e.equals(null);
    }
}

interface Employee {
}
 ```
 首先接口与Object没有继承关系。其次接口对于Object中的每个public方法都有一个隐式声明，如果对 `final` 方法覆盖，则会编译错误。
 参考：<http://docs.oracle.com/javase/specs/jls/se7/html/jls-9.html#jls-9.2>

 <!-- more -->