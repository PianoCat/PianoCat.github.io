---
layout: post
title: leetcode-80 Remove Duplicates from Sorted Array II
category: 算法
tags: [leetcode, Array, Two Pointers]
---

### leetcode-80 Remove Duplicates from Sorted Array II ###

* 题目描述

Follow up for "Remove Duplicates":
What if duplicates are allowed at most twice?

For example,
Given sorted array nums = `[1,1,1,2,2,3]`,

Your function should return length = `5`, with the first five elements of nums being `1`,`1`,`2`,`2` and `3`. It doesn't matter what you leave beyond the new length.

+ C++解法

这道题目没什么好说的了，有了上一道题作为基础，这道题很简单。

```cpp
class Solution
{
public:

	int removeDuplicates(vector<int>& nums) {
		if (nums.size() < 1)
			return 0;
		else if (nums.size() == 1)
			return 1;
		else if (nums.size() == 2)
			return 2;
		else{
			int flag = 0;
			for (vector<int>::iterator i = nums.begin() + 2; i != nums.end();){
				int temp = nums.at(flag);
				if (*i == temp){
					i = nums.erase(i);
				}
				else{
					temp = nums.at(++flag);
					i++;
				}
			}
			return nums.size();
		}

	}

};
```
