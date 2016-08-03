---
layout: post
title: leetcode-153 Find Minimum in Rotated Sorted Array
category: 算法
tags: [Array, Binary Search, leetcode]
---

### leetcode-153 Find Minimum in Rotated Sorted Array ###

* 题目描述

Suppose a sorted array is rotated at some pivot unknown to you beforehand.

(i.e.,`0 1 2 4 5 6 7` might become `4 5 6 7 0 1 2`.

Find the minimum element.

You may assume no duplicate exists in the array.

* C++解法一

先排序，再选出最小值，时间复杂度为`O(nlogn)`，用时8ms。

```cpp
class Solution {
public:
    int findMin(vector<int>& nums) {
        sort(nums.begin(),nums.end());
		return nums[0];
    }
};
```

* C++解法二

直接查找，时间复杂度为`O(n)`，用时4ms。

```cpp
class Solution {
public:
    int findMin(vector<int>& nums) {
        int ret = nums[0];
		for (int i = 1; i < nums.size(); ++i){
			if (nums[i] < ret)
				ret = nums[i];
			else
				continue;
		}
		return ret;
    }
};
```

* C++解法三

其实看到这种题目，最开始应该想到的应该就是二分法，这样时间效率是最好的，时间复杂度为`O(logn)`，用时4ms。

```cpp
class Solution {
public:
    int findMin(vector<int>& nums) {
        int size = nums.size()-1;
		int l = 0;
		int r = size;
		while (l <= r){
			int mid = l + (r-l) / 2;
			if (nums[mid] > nums[size])
				l = mid + 1;
			else
				r = mid - 1;
		}
		return nums[l];
    }
};
```
