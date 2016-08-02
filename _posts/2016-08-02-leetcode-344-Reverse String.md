---
layout: post
title: leetcode-344 Reverse String
category: 算法
tags: [leetcode]
---

### leetcode-344 Reverse String ###

* 题目描述

Write a function that takes a string as input and returns the string reversed.

<b>Example:</b>

Given s = "hello", return "olleh".

* C++解法

从string的两边往中间走，边走边交换。算法用时12ms。

```cpp
class Solution {
public:
	string reverseString(string s) {
		int left = 0, right = s.size() - 1;
		while (left < right){
			char temp = s[left];
			s[left++] = s[right];
			s[right--] = temp;
		}
		return s;
	}
};
```
