title:  Swing 笔记
description: Swing 学习笔记
date: 2015-07-19
tags:  [Java,Swing]
categories:  [Java]

--------------------

# 界面设计工具包
AWT、Swing、SWT  3种工具包，**Swing最好**

# 类层次
3种窗体 ： JFrame、JDialog、JWindow
×××Model 组件模型基类
JComponent 组件基类
×××UI 设置样式

# 界面消息提示JOptionPane
showConfirmedDialog显示确认对话框

# Swing 菜单 JMenu
JMenuBar、JMenu、JMenuItem
后两者之间的关系类似于文件夹和文件

Menu的事件应该用Actionlistener而非MouseListener

# 自定义绘图组件
**Graphic 、Graphic2D 优先使用后者**，，能消除锯齿，且方法更多
drawXXX方法绘图，fillXXX方法填充
LookAndFeel改变界面的样式，Nis***最好，一般是System默认

每次组件更新都会调用paint函数
paint函数也会依次调用paintComponent（绘制自身）、paintBorder（绘制边界）和paintChildren（绘制子对象）

# 布局管理器 Layout

absolute、flow、border、grid、group 主要有这五中，**最后一种最好用**

# 文件选择器JFileChooser

setFileSelectionMode 可设置是否能够选择目录
setMultiSelectionEnabled 可设置是否能够多选

showOpenDialog 和 showSaveDialog  打开文件选择器，根据返回值做不同处理
getSelectedFile 和 getSelectedFiles获取选择的文件，后者用于多选情况

FileNameExtensionFilter文件扩展名过滤器
**setFilter需要再show×××Dialog之前**