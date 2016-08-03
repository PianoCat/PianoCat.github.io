---
layout: post
title: leetcode-53 Maximum Subarray
category: 算法
tags: [leetcode, Array, Dynamic Programming, Divide and Conquer]
---

### leetcode-53 Maximum Subarray ###

* 题目描述

Find the contiguous subarray within an array (containing at least one number) which has the largest sum.

For example, given the array `[−2,1,−3,4,−1,2,1,−5,4]`,

the contiguous subarray`[4,−1,2,1]` has the largest sum = `6`.

* C++解法

求数组的最大子序列，这是一道很经典的动态规划题目，这里就不再介绍暴力求解`O(n^2)`和分治算法`O(nlogn)`了。下面的代码是比较简练的一种代码，很简单，能很快看懂，时间复杂度为`O(n)`，代码耗时`12ms`。

```cpp
class Solution {
public:
	int maxSubArray(vector<int>& nums) {
		int sum = nums[0];
		int temp = 0;

		for (int i = 0; i < nums.size(); ++i){
			if (temp < 0)
				temp = nums[i];
			else
				temp += nums[i];
			if (temp>sum)
				sum = temp;
		}

		return sum;
	}
};
```
