---
layout: post
title: leetcode-81 Search in Rotated Sorted Array II
category: 算法
tags: [leetcode, Array, Binary Search]
---

### leetcode-81 Search in Rotated Sorted Array II ###

* 题目描述

Follow up for "Search in Rotated Sorted Array":
What if duplicates are allowed?

Would this affect the run-time complexity? How and why?

Write a function to determine if a given target is in the array.

+ C++解法

同样的，这道题目也用二分法来解答，用时16ms。

```cpp
class Solution
{
public:

	bool search(vector<int>& nums, int target) {
		int size = nums.size();
		while (size >= 1){
			int mid = nums[size / 2];
			int start = nums[0];
			int end = nums[size - 1];

			if (target == mid){
				return true;
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
					return false;
				else
					return flag;
			}
			else if ((nums.size() != 1 && start >= nums[size / 2 - 1]) || (nums.size()>2 && nums[size / 2 + 1] >= end)){
				vector<int> next,next1;
				for (int i = 0; i < size / 2; ++i){
					next.push_back(nums.at(i));
				}
				for (int j = size / 2 + 1; j < size; ++j){
					next1.push_back(nums.at(j));
				}
				int flag1 = search(next1, target);
				int flag = search(next, target);
				return (flag || flag1);
			}
			else{
				return false;
			}
		}
		return false;
	}

};
```
