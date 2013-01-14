---
title: Java实现Shell(希尔)排序
author: wahyd4
comments: true
layout: post
permalink: /2012/09/java-shell-sorting/
categories:
  - java
  - 未分类
tags:
  - java
  - 希尔排序
  - 算法
---
> 如需下载源代码，请到github：<https://github.com/wahyd4/java-sorting>

Shell(希尔)排序是建立在直接插入排序基础上之上的，只是它会先将这个数组按照一定的间隔分成若干个小数组先进行直接插入排序。以先比较较远的元素，再比较较近的元素，最后比较相邻的元素。可以逐步减小比较的次数。其时间复杂度优于直接插入排序。

更多的信息请查看[百度百科][1]或者[维基百科][2]的介绍。下面上希尔排序的代码：

<pre class="brush: java; title: ; notranslate" title="">public class ShellSort {

	// 定义需要排序的数组
	private static int[] data = { 16, 20, 1, 6, 3, 19, 7, 14, 5, 60, 29, 40 };

	public static void shellSort(int[] data) {
		//获取数组长度
		int length = data.length;
		// 首先进行分组,每次组中元素为之前1/2。
		for (int gap = length / 2; gap &gt; 0; gap = gap / 2) {
			// 对每个组进行插入比较
			for (int i = gap; i &lt; length; i++) {
   	                     for (int j = i; j &gt;= gap && data[j] &lt; data[j - gap]; j = j- gap) {
					//缓存下表最大的那个数
					int temp = data[j];
					//将两数交换位置，将较大数保存到下标最大的位置。
					data[j] = data[j - gap];
					data[j - gap] = temp;
				}

			}
		}
	}

	public static void main(String[] args) {
		shellSort(data);
		for (int flag : data) {
			System.out.print(flag + " ");
		}
	}

}
</pre>

虽然代码里面希尔排序是三层循环，但是只有中间层循环才是n数量级，外层循环为lbn,最里程循环也远小于n.平均时间复杂度还优于直接插入排序。

 [1]: http://baike.baidu.com/view/178698.htm
 [2]: http://zh.wikipedia.org/zh/%E5%B8%8C%E5%B0%94%E6%8E%92%E5%BA%8F
