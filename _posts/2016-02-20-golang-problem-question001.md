---
layout: post
title: Go编程题目：1、Multiples of 3 and 5（3和5的倍数）
categories: [IT]
tags: [golang]
fullview: true
---

# Question
If we list all the natural numbers below 10 that are multiples of 3 or 5, we get 3, 5, 6 and 9. The sum of these multiples is 23.

Find the sum of all the multiples of 3 or 5 below 1000.

如果我们列出所有自然数低于10且为3或5的倍数,可以得到3、5、6和9。这些倍数的总和是23。
找到3或5的倍数的总和1000以下。

# 解题算法

3的倍数相加可以简化为：

	3+6+9+12+......+999=3*(1+2+3+4+...+333)

同理，5的倍数：

	5+10+15+...+995=5*(1+2+....+199)

根据规律可以简化为：

	// target = 除数（999），n = 被除数（3、5）
	p  = target / n
	sum = n * (p * (p + 1)) / 2

因此，程序为：


	var target = 999

	func sumDivision(n int) int {
		p := target / n
		return n * (p * (p + 1)) / 2
	}

	func main() {
		sum := sumDivision(3) + sumDivision(5) - sumDivision(15)

		fmt.Println(sum)
	}

结果为：233168