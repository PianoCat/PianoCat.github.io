---
layout: post
title: leetcode-371 Sum of Two Integers
category: 算法
tags: [leetcode, Bit Manipulation, 剑指offer]
---

### leetcode-371 Sum of Two Integers ###

* 题目描述

Calculate the sum of two integers a and b, but you are not allowed to use the operator + and -.

**Example:**

Given a = 1 and b = 2, return 3.

* 解法一

这道题目不允许用`+`和`-`，那么只能用位运算来计算加法了。首先判断要不要进位，记录为carry；然后利用异或运算符`^`来保存结果到a，最后把进位值左移一位；重复操作直到进位为0。用时0ms。

```cpp
class Solution {
public:
	int getSum(int a, int b) {
		while (b){
			int carry = a&b;
			a = a^b;
			b = carry << 1;
		}
		return a;
	}
};
```

* 解法二

大神的解法。。用时0ms。

首先当a&b = 0 时 return a| b ， a&b = 1 时 return 一个递归式；

a&b = 0 的情况很好理解：当任何一个加数等于0时，返回另外一个加数即可

递归式比较复杂：

先看异或（^，开始当成了乘方，纠结了好久）运算：  0 ^ 0 = 0    0 ^ 1 = 1   1 ^ 0 = 1   1 ^ 1 = 0

　　　　　　　　　　　　　  再看加法的进位运算：  0 + 0 = 1    0 + 1 = 1   1 + 0 = 1    1 + 1 = 0(进位)

除了进位的话结果完全一样，所以如果没有进位的话，我们可以直接用异或替代加法。

再考虑进位运算， 只有当 两位都是1 时才会进位， 那么通过与运算& 我们就可以得到所有两个数都为1 的位，由于进位是要加到高位上的，

所以我们再把与之后的结果左移一位，与异或后的结果相加，就可以得到完整的加法结果，

在递归过程中，一个参数表示异或的结果，另一个表示进位的结果，那么递归的终点呢？

就是不再进位，由于两个数是有限长度的，在经过最多32次循环后肯定不再需要进位，那么其中一个参数就会为0，我们就得到了最终的结果了。

```cpp
class Solution {
public:
	int getSum(int a, int b) {
		return a&b ? getSum((a&b) << 1, a^b) : a | b;
	}
};
```
