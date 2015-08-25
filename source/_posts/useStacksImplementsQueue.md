title: 用两个栈实现队列
description: 用两个栈实现队列
date: 2015-07-27
tags:  [算法]
categories:  [算法]

------------------------
# 题目
>用两个栈实现队列

# 解法
1. stack1 为进栈，添加数据都push到本栈
2. stack2 为出栈，删除数据都从本栈pop。
 如果删除时 stack2 为空而 stack1 不为空，则先将stack1中的数据全部 pop 出来依次 push 到 stack2 中，然后再从 stack2 pop。

# 举一反三
也可使用两个队列实现栈，方法类似。

