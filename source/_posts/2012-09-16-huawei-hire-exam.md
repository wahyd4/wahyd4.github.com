---
title: 华为一个字符串处理的上机题
author: wahyd4
comments: true
layout: post
permalink: /2012/09/huawei-hire-exam/
categories:
  - java
tags:
  - java
  - 华为
  - 算法
---
昨天下午参加了华为的上机笔试，3道题，但是答得不是很理想，回来有好好思考了一些，现在这里把相对较难的那道题分享一下。题目是这样的：

问题描述：

> 在给定字符串中找出单词（ “单词”由大写字母和小写字母字符构成，其他非字母字符视为单词的间隔，如空格、问号、数字等等；另外单个字母不算单词）；找到单词后，按照长度进行降序排序，（排序时如果长度相同，则按出现的顺序进行排列），然后输出到一个新的字符串中；如果某个单词重复出现多次，则只输出一次；如果整个输入的字符串中没有找到单词，请输出空串。输出的单词之间使用一个“空格”隔开，最后一个单词后不加空格。
> 
> 要求实现函数：
> 
> void my_word(charinput[], char output[])
> 
> 【输入】  char input[], 输入的字符串
> 
> 【输出】  char output[]，输出的字符串
> 
> 【返回】 无
> 
> 示例
> 
> 输入：charinput[]=”some local buses, some1234123drivers” ，
> 
> 输出：charoutput[]=”drivers local buses some”
> 
> 输入：charinput[]=”%A^123 t 3453i*()” ，
> 
> 输出：charoutput[]=”"

乍一看，题目的确不怎么难，但是其中隐藏着很多细节。我的思考是这样的：

1.  首先分离其中的字符串（单词），需要注意的是单个字母不能成为单词，当到达字符串末尾时，即使没有符号，也需要分离单词。
2.  其次是排除其中的重复单词（java里使用 Set实现，set中不能出现重复的内容）
3.  对单词进行排序，按照单词长度逆序，如果单词的长度相同，则按照单词出现的先后顺序排序。在项目中我使用的是选择排序，时间复杂度略小于o(n*n)
4.  输出数据，如果没有单词输出”"

下面贴出我实现的代码，如发现有什么问题，请指出：

<pre class="brush: java; title: ; notranslate" title="">package com.toozhao.test;

import java.util.HashSet;
import java.util.Set;

/**
 * {@link} http://toozhao.com
 * @author Junv
 *
 */
public class MyWord {

	/**
	 * @param args
	 */
	public static void main(String[] args) {
		MyWord test = new MyWord();
		System.out
				.println(test.process("some local buses, some1234123drivers"));
	}

	/**
	 * 将输入信息通过处理，使其满足要求。并返回
	 * 
	 * @param input
	 * @return
	 */
	public String process(String input) {
		char[] array = input.toCharArray();

		Set&lt;String&gt; list = new HashSet&lt;String&gt;();
		int mark = 0;// 用于标记当前截断位置

		boolean formerIsChar = false; // 设置上一个是否是字符
		for (int i = 0; i &lt; array.length; i++) {

			// 说明不是字母
			if (array[i] &lt; 65 || array[i] &gt; 122
					|| (array[i] &gt; 90 && array[i] &lt; 97)) {
				// System.out.println(array[i]);

				// 如果上一个数为字符,且单词长度不能为1
				if (formerIsChar == true && (i!= mark+1)) {
					char[] temp = new char[i - mark];
					System.arraycopy(array, mark, temp, 0, i - mark); // 复制数组
					list.add(this.getStr(temp)); // 添加到list中

				}

				mark = i + 1; // 标记为下一个字符开始的脚标
				formerIsChar = false;
			} else {
				// 说明上一个是字符
				formerIsChar = true;

				// 处理最后的字符串，即使不是非字符也需要截断
				if (i == array.length - 1) {
					char[] temp = new char[i - mark + 1];
					System.arraycopy(array, mark, temp, 0, i - mark + 1);
					list.add(this.getStr(temp));
				}
			}

		}

		// 如果为空则返回空格
		if (list.size() == 0) {
			return "";
		}

		String[] myArray = new String[list.size()];
		// 将list转为数组
		list.toArray(myArray);
		// 对数组排序
		this.sort(myArray);

		// 遍历得到结果
		StringBuilder sb = new StringBuilder();
		for (int j = 0; j &lt; myArray.length; j++) {
			sb.append(myArray[j]);
			sb.append(" ");
		}
		return sb.toString();
	}

	/**
	 * 将字符数组转成字符串
	 * 
	 * @param charStr
	 * @return
	 */
	public String getStr(char[] charStr) {
		StringBuilder sb = new StringBuilder();
		for (int i = 0; i &lt; charStr.length; i++) {

			sb.append(charStr[i]);
		}
		return sb.toString();
	}

	/**
	 * 按照长度降序，如果长度相同，则比较谁更先出现。&lt;br&gt;
	 * 使用的是选择排序
	 * @param original
	 * @return
	 */
	public String[] sort(String[] original) {

		for (int i = 0; i &lt; original.length - 1; i++) {
			int temp = i;
			for (int j = i + 1; j &lt; original.length; j++) {
				// 如果后面的长度大于前面
				if (original[j].length() &gt; original[i].length()) {
					temp = j;
				}

				// 如果长度相同，则看谁出现得早
				if (original[j].length() == original[i].length()) {
					if (j &gt; i) {
						temp = j;
					}
				}
			}

			if (temp != i) {
				String tempStr = original[i];
				original[i] = original[temp];
				original[temp] = tempStr;
			}
		}
		return original;
	}

}

</pre>

 
