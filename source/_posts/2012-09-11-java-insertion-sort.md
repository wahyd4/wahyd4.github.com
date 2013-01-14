---
title: Java 实现直接插入排序
author: wahyd4
comments: true
layout: post
permalink: /2012/09/java-insertion-sort/
categories:
  - java
tags:
  - java
  - 直接插入排序
  - 算法
---
> 项目代码已经发布到github.欢迎各位下载：<https://github.com/wahyd4/java-sorting>

快到校招了，我还是把以前的数据结构的书拿出来复习了，不过这次我将用java 来实现数据结构中的一些算法。当然还是希望能够顺利通过这些公司的笔试。下面分享的是直接插入排序。

<pre class="brush: java; title: ; notranslate" title="">public class InsertionSort {

// 定义需要排序的数组
private static int[] array = { 1, 20, 6, 3, 19, 7, 14, 12, 10 };

public static void main(String args[]) {

for (int outer = 1; outer &lt; array.length; outer++) {
  int temp = array[outer];
  for (int inner = outer - 1; inner &gt;= 0 && temp &lt; array[inner]; inner--) {

    /**
    * 将最大的赋值给目前比较的数组尾部 由于这里的数组下标需要
    *  跟随循环而变化，所以只能使用 j来表示
    */
    array[inner + 1] = array[inner];
    // 重新赋值第二大的数
    array[inner] = temp;
    // 重新赋值参考值，接着下标-1
    temp = array[inner];
  }
}
   // 便利排序后的数组
   for (int flag : array) {
     System.out.println(flag);
   }
 }
}

</pre>

**算法的时间复杂度：**

直接排序最糟糕时需要比较的次数为（若数组长度为n）:1+2+…+n-1=n(n-1)/2,复杂度为O（n2），一般情况下，复杂度也是如此。
