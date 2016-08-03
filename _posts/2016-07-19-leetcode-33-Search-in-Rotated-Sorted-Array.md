---
layout: post
title: leetcode-33 Search in Rotated Sorted Array
category: 算法
tags: [leetcode, Binary Search, Array]
---

### leetcode-33 Search in Rotated Sorted Array ###

* 题目描述

Suppose a sorted array is rotated at some pivot unknown to you beforehand.

(i.e., `0,1,2,4,5,6,7` might become `4,5,6,7,0,1,2`).

You are given a target value to search. If found in the array return its index, otherwise return -1.

You may assume no duplicate exists in the array.

+ C++解法

看起来是挺简单的，然而做了半天发现有情况没有考虑完全，还是略麻烦的。最后Runtime是4ms，先post一下自己写的...

```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int size = nums.size();
		while (size >= 1){
			int mid = nums[size / 2];
			int start = nums[0];
			int end = nums[size - 1];

			if (target == mid){
				return size / 2;
			}
			else if (nums.size() != 1 && target >= start && target <= nums[size / 2 - 1] && start <= nums[size / 2 - 1]){
				vector<int> next;
				for (int i = 0; i < size / 2; ++i){
					next.push_back(nums.at(i));
				}
				return search(next, target);
			}
			else if (nums.size() > 2 && target >= nums[size / 2 + 1] && target <= end && nums[size / 2 + 1]<=end){
				vector<int> next;
				for (int j = size / 2 + 1; j < size; ++j){
					next.push_back(nums.at(j));
				}
				int flag = search(next, target);
				if (flag == -1)
					return -1;
				else
					return (size / 2 + 1) + flag;
			}
			else if (nums.size() != 1 && start>nums[size / 2 - 1]){
				vector<int> next;
				for (int i = 0; i < size / 2; ++i){
					next.push_back(nums.at(i));
				}
				return search(next, target);
			}
			else if (nums.size()>2 && nums[size / 2 + 1]>end){
				vector<int> next;
				for (int j = size / 2 + 1; j < size; ++j){
					next.push_back(nums.at(j));
				}
				int flag = search(next, target);
				if (flag == -1)
					return -1;
				else
					return (size / 2 + 1) + flag;
			}
			else{
				return -1;
			}
		}
		return -1;
    }
};
```
其实还有一种思路很容易想到，可以先将vector排序，之后找到target，然后再找到对应的原始index，这个后面有时间再实现一下。
