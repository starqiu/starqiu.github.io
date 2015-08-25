title:  Git笔记
description: Git笔记
date: 2015-08-11
tags:  [Git]
categories:  [Git]

----------------------

1.  <font color=red>如何在命令行显示版本树</font>
 使用`git log --graph --oneline --all`  ， 效果如下：
 ![命令行中的版本树](/images/gitTree.png)
 为方便书写，可以使用以下命令设置别名
 `git config --global alias.tree "log --oneline --decorate --all --graph"`
 然后我们就可以输入命令`git tree` 就可以达到同样的效果了
 参考：<http://stackoverflow.com/questions/1064361/unable-to-show-a-git-tree-in-terminal>
