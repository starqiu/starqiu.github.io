title:  R笔记
description: 使用R时遇到的问题及解决方案
date: 2015-07-18
tags:  [R]
categories:  [R]

--------

1. <font color=red>如何对数组去重？</font>
 使用 `duplicated` 函数是一个可以用来解决向量或者数据框重复值的函数，它会返回一个TRUE和FALSE的向量，以标注该索引所对应的值是否是前面数据所重复的值。
 需要注意的是不重复对应返回的值是FALSE，所以在后面我们用!来取反以得到不重复的值。
 ```R
arr <- c(1,2,3,5,3,2,4,1,5)
arr[!duplicated(arr)]
 ```
  输出为：
  [1] 1 2 3 5 4
2. <font color=red>如何取得数组的极大值（或极小值）</font>
 使用 `diff` 和 `sign` 两个函数。其中`diff` 得到相邻数的差， `sign` 则取符号位（-1,0,1），因每次 `diff` 返回的数组比原数组的长度小于1，我们主动在首位添加1，表示最小值，即不论原来首位是什么数，都比新添加的数大，在尾部添加-1表示最大值。
 所谓极大值，即该值比相邻两边的值都大 ，第一次`diff`要比左边的值大，比右边的值小，所以`diff`后的值应该是1，-1（没有考虑相等的情况）；那第二次`diff`的值应该是`-1-1=-2`.
 代码如下：
 ```r
 findMaxima <- function(array){
  which(diff(c(1,sign(diff(array)),-1)) == -2)
}
 ```
 返回的是index
 ```r
 arr <- c(1,2,3,5,3,2,4,1,5)
 findMaxima(arr)
 ```
 运行结果为：
 [1] 4 7 9
3. <font color="red">如何获得当前文件所在的目录</font>
 ```r
 curFileDir <- dirname(sys.frame(1)$ofile)
 ```
 需要注意的是这行代码在命令行运行会出错，只能在文件里面执行。<!-- more -->

4. <font color="red"> = and <- 在R中的区别</font>
 它们都可以用来赋值，区别主要有以下3点
 + **在函数内部，范围不同。**‘=’只能在函数内使用，‘<-’在函数外依然能够使用
    ```R
    median(x = 1:10)
    x 
    ## Error: object 'x' not found
    ```
    这种情况下，x的作用域在函数内部而不是用户的工作空间
     ```
    median(x <- 1:10)
    x 
    ## [1] 1 2 3 4 5 6 7 8 9 10
     ```
     这种情况下，x的作用域在用户的工作空间，x在函数外依然能够使用
 + **'<-' 的运算优先级比‘=’高**
    ` x <- y =5`  是错的
     `x <- (y=5)` 及 `x = y <- 5` 是对的
 + **‘<-'更容易混淆( 对比’< -‘)**
    `x<-5` 是赋值还是比较？（赋值），猜想：最长字串解析法

5. <font color=red>如果文件使用 `commandArgs` 读取参数，在 `source` 时如何给它传参数？</font>
 * 覆盖 `commandArgs` 函数
    file_to_source.R ：
     ```R
      args <- commandArgs(TRUE)
      print(args)
    ```

    file_to_test_source.R :
     ```R
    commandArgs <- function(trailingOnly=FALSE) c(1,2,3) 
    curFileDir <- dirname(sys.frame(1)$ofile) #get current file directory
    source(file.path(curFileDir,"file_to_source.R"))
    ```
    执行file_to_test_source.R文件，打印出 ：
    [1] 1 2 3

 * 使用 `system` 函数替代 `source` 函数
    file_to_test_source2.R :
    ```R
    curFileDir <- dirname(sys.frame(1)$ofile) #get current file directory
      system(paste("Rscript",file.path(curFileDir,"file_to_source.R"),1,2,3))
    ```
    执行file_to_test_source2.R文件，打印出 ：
    [1] "1" "2" "3"

6. <font color=red>R中如何查找函数源码？（寻找.R 文件）</font>

 使用搜索引擎搜 site:https://svn.r-project.org/R/trunk/src `functionname`
 参考：<http://stackoverflow.com/questions/1439348/how-to-examine-the-code-of-a-function-in-r-thats-object-class-sensitive#answer-1444512>
