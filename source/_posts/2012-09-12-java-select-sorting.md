---
title: java实现选择排序
author: wahyd4
comments: true
layout: post
permalink: /2012/09/java-select-sorting/
categories:
  - java
tags:
  - java
  - 算法
  - 选择排序
---
选择排序大概的思想就是，每一次循环找出需要排序的部分中最小的那个数，找出只有再将最小的那个数移动到它应该放置的那个位置。因为虽然他的遍历次数也是1+2+3+…+n-1,不过它每次循环只交换一次，总的来说效率还是比直接插入排序好一些。更详细的解释参考[百度百科][1]和[维基百科][2]。

下面上代码吧：

<pre class="brush: java; title: ; notranslate" title="">package com.toozhao.sort;

/**
 *
 * @author Junv
 *
 */
public class SelectSort {
	// 定义需要排序的数
	private static int[] array = { 10, 50, 8, 29, 30, 17, 12, 40, 32, 7, 4, 22 };

	public static void main(String args[]) {
		sort(array);
		for (int flag : array) {
			System.out.print(flag + " ");
		}
	}

	public static void sort(int[] data) {
		// 外层循环一次，找到i to (data.length-1)这个数组中最小的一个数。
		for (int i = 0; i &lt; (data.length - 1); i++) {
			// temp用来标注值最小的那个数。
			int temp = i;
			for (int j = i + 1; j &lt; data.length; j++) {
				// 将temp 始终标记为最小那个数。
				if (data[j] &lt; data[temp]) {
					temp = j;
				}
			}
			// 如果i != temp 说明，最小那个数为data[temp],则交换。
			if (i != temp) {
				int t = data[i];
				data[i] = data[temp];
				data[temp] = t;
			}
		}
	}
}

</pre>

如需下载完整代码，以及其他排序代码，请到：

> <pre>github：https://github.com/wahyd4/java-sorting</pre>

 [1]: http://baike.baidu.com/view/547263.htm
 [2]: http://zh.wikipedia.org/zh/%E9%80%89%E6%8B%A9%E6%8E%92%E5%BA%8F
