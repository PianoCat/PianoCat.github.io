---
layout: post
title: leetcode-258 Add Digits
category: 算法
tags: [leetcode]
---

### leetcode-258 Add Digits ###

* 题目描述

Given a non-negative integer `num`，repeatedly add all its digits until the result has only one digit.

For example:

Given `num = 38`, the process is like:`3 + 8 = 11`,`1 + 1 = 2`. Since `2`has only one digit, return it.

**Follow up:**

Could you do it without any loop/recursion in O(1) runtime?

* C++解法一

耗时8ms。

```cpp
class Solution {
public:
	int addDigits(int num) {
		int n = count(num);
		int sum = 0;
		while (n > 0){
			sum += num % 10;
			num /= 10;
			n--;
		}
		if (count(sum) == 1)
			return sum;
		else
			return addDigits(sum);
		return 0;
	}

	int count(int num){
		int count = 1;
		while (num / 10 != 0){
			count++;
			num = num / 10;
		}
		return count;
	}
};
```

* C++解法二

题目提示有`O(1)`的解法，但是这个问题应该是个数学问题，想了好久也得不到结果。后来在[wiki](https://en.wikipedia.org/wiki/Digital_root)找到了答案。只需要按照下面这个公式来编程即可得到答案，用时8ms。

![img](https://raw.githubusercontent.com/PianoCat/Blog_imgs/master/images_2016/digital_root.png)

```cpp
class Solution {
public:
    int addDigits(int num) {
        int ret = 0;
		ret = 1 + (num - 1) % 9;
		return ret;
	}
};
```
