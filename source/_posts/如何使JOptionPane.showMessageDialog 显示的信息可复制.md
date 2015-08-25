title:  如何使JOptionPane.showMessageDialog 显示的信息可复制
description: 如何使JOptionPane.showMessageDialog 显示的信息可复制
date: 2015-08-24
tags:  [Java]
categories:  [Java]

----------------------
> 如何使JOptionPane.showMessageDialog 显示的信息分行显示且可复制?
> 
 
# 分析
 1. 使用`JTextArea`，并将其设为不可编辑，使用其克复制功能
 2. 调用`setLineWrap`和`setWrapStyleWord`方法使`JTextArea`按单词计数分行显示
 3. 调用`setHorizontalScrollBarPolicy(ScrollPaneConstants.HORIZONTAL_SCROLLBAR_NEVER)`使得水平滑动按钮消失。

# 代码
 ```java
    /**
     * 显示错误信息提示框，以便提示用户错误信息
     * @param errorMsg 错误信息
     */
    public static void showErrorDialog(String errorMsg){
         // create a JTextArea
          JTextArea textArea = new JTextArea(6, 25);
          textArea.setText(errorMsg + ErrorMsg.SEE_ERROR_LOG );
          textArea.setEditable(false);
          textArea.setWrapStyleWord(true);
          textArea.setLineWrap(true);
          textArea.setCaretPosition(0);
           
          // wrap a scrollpane around it
          JScrollPane scrollPane = new JScrollPane(textArea);
          scrollPane.setHorizontalScrollBarPolicy(ScrollPaneConstants.HORIZONTAL_SCROLLBAR_NEVER);
//      String msg = CommonUtils.divideIntoMultiLines(errorMsg + ErrorMsg.SEE_ERROR_LOG, 20)  ;
          JOptionPane.showMessageDialog(null,scrollPane ,  "错误信息", JOptionPane.ERROR_MESSAGE);
    }
 ```