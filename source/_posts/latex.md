title: Latex 笔记
description: 使用LaTeX在博客上写数学公式
date: 2015-07-20
mathjax: true
tags: [LaTeX ]
categories: [LaTeX ]
---
# 在博客上写LaTex数学公式
 参见[在博客上写LaTex数学公式](http://wuchong.me/blog/2014/03/14/use-latex-in-blog/)
#LaTeX数学公式输入
## 标识
 `$math_expression$` 或 `\( math_expression \)` 表示内嵌公式
 `$$math_expression$$` 或 `\[math_expression \]` 表示公式独占一行
 `\begin{equation} math_expression \end{equation}`，则公式除了独占一行还会自动被添加序号， 如何公式不想编号则使用 `\begin{equation*} math_expression \end{equation*}`。

## 字符转义
　对于特殊字符`# $ % & ~ _ ^ \ { }`，在前面加转义符`\`，表示原字符

## 上标和下标
 用 ^ 来表示上标，用 _ 来表示下标，看一简单例子：
 ```
 $$\sum_{i=1}^n a_i=0$$
 $$f(x)=x^{x^x}$$ //上下标可以嵌套
 ```
 效果:
$$\sum_{i=1}^n a_i=0$$
$$f(x)=x^{x^x}$$

## 数学符号及公式
参见[常用数学符号的 LaTeX 表示方法](http://mohu.org/info/symbols/symbols.htm) <!-- more -->

## 插入文本
 通过 \mbox{text} 在公式中添加text，比如：
 ```latex
    $$\mbox{对任意的$x>0$}, \mbox{有 }f(x)>0. $$
 ```
 效果:
$$\mbox{对任意的$x>0$}, \mbox{有 }f(x)>0. $$

## 分数及开方
 ```
\frac{numerator}{denominator} //表示分数
\sqrt{expression} //表示开平方，
\sqrt[n]{expression} //表示开 n 次方.
 ```
  效果：
 $$\frac{numerator}{denominator} $$
 $$\sqrt{expression_{a_b}}$$
 $$\sqrt[n]{expression^{a_b}} $$


 ## 省略号（3个点）
 \ldots 表示跟文本底线对齐的省略号；\cdots 表示跟文本中线对齐的省略号
 \dots效果 : $ x + \dots + y$
 \ldots效果 : $ x + \ldots + y$
 \cdots效果 : $ x + \cdots + y$
 ```
$$f(x_1,x_x,\ldots,x_n) = x_1^2 + x_2^2 + \cdots + x_n^2 $$
 ```
 效果：
 $$f(x_1,x_x,\ldots,x_n) = x_1^2 + x_2^2 + \cdots + x_n^2 $$

 ## 括号和分隔符
 () 和 [ ] 和 ｜ 对应于自己；
 {} 对应于 \{ \}；
 || 对应于 \|。
 当要显示大号的括号或分隔符时，要对应用 \left 和 \right，如：
    \[f(x,y,z) = 3y^2 z \left( 3 + \frac{7x+5}{1 + y^2} \right).\]
 效果：
$$f(x,y,z) = 3y^2 z \left( 3 + \frac{7x+5}{1 + y^2} \right).$$

## 多行的数学公式
 ```
\begin{eqnarray*}
\cos 2\theta & = & \cos^2 \theta - \sin^2 \theta \\
                      & = & 2 \cos^2 \theta - 1.
\end{eqnarray*}
 ```
 其中&是对其点，表示在此对齐。
 \*使latex不自动显示序号，如果想让latex自动标上序号，则把\*去掉

## 矩阵
 ```
$$ \left( \begin{array}{ccc}
a & b & c \\\\
d & e & f \\\\
g & h & i \end{array} \right)$$
 ```
 效果：
$$ \left( \begin{array}{ccc}
a & b & c \\\\
d & e & f \\\\
g & h & i \end{array} \right)$$
 c表示向中对齐，l表示向左对齐，r表示向右对齐。

## 导数、极限、求和、积分
 导数由\partial表示。`$\frac{\partial u}{\partial t}$`表示 $\frac{\partial u}{\partial t}$ .
 极限由\lim表示。
 ```
    $$\lim_{x \to +\infty}$$
 ```
$$\lim_{x \to +\infty}$$

 ```
    $$\inf_{x > s}$$
 ```
$$\inf_{x > s}$$

 ```
    $$\sup_K$$
 ```
$$\sup_K$$ 
 求和符号与积分符号的命令分别为 \sum 和 \int，它们通常都有上下限，在排版上就是上标和下标。

 ```
  $$\sum_{i=1}^{2n}$$
 ```
$$\sum_{i=1}^{2n}$$

 ```
  $$\int_a^b f(x) dx$$
 ```
$$\int_a^b f(x) dx$$

# 参考文献
1.  [LaTeX技巧10：LaTeX数学公式输入初级入门](http://blog.sina.com.cn/s/blog_5e16f1770100fs38.html)
2. 数学函数参考手册:[常用数学符号的 LaTeX 表示方法](http://mohu.org/info/symbols/symbols.htm)
3. [在博客上写LaTex数学公式](http://wuchong.me/blog/2014/03/14/use-latex-in-blog/)


