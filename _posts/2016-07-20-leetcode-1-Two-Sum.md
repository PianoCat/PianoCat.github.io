---
layout: post
title: leetcode-1 Two Sum
category: 算法
tags: [leetcode, Array, Hash Table]
---

### leetcode-1 Two Sum ###

* 题目描述

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution.

Example:

```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

* C++解法一

最容易想到的就是暴力解法，时间复杂度为`O(n^2)`，用时664ms，惨不忍睹。

```cpp
class Solution {
public:
	vector<int> twoSum(vector<int>& nums, int target) {
		vector<int> result;
		for (int j = 0; j < nums.size() - 1; ++j){
			int temp = nums[j];
			for (int k = j+1; k < nums.size(); ++k){
				if ((temp + nums[k]) == target){

					result.push_back(j);
					result.push_back(k);
					return result;
				}
				else
					continue;
			}
		}
		return result;
	}
};
```

* C++解法二

先对vector做一次排序，用时`O(nlogn)`，然后再用双指针向中间夹逼，最终的复杂度也是`O(nlogn)`，最终用时12ms。

```cpp
class Solution {
public:
	vector<int> twoSum(vector<int>& nums, int target) {
		vector<int> result;
		vector<int> sorted(nums);

		sort(sorted.begin(), sorted.end());

		int left = 0, right = sorted.size() - 1, sum = 0;
		while (left < right){
			sum = sorted[left] + sorted[right];
			if (sum == target){
				for (int i = 0; i < sorted.size(); ++i){
					if (nums[i] == sorted[left])
						result.push_back(i);
					else if (nums[i] == sorted[right])
						result.push_back(i);
					if (result.size() == 2)
						return result;
				}
			}
			else if (sum>target){
				--right;
			}
			else{
				++left;
			}
		}
		return result;
	}
};
```

* C++解法三

可以维护一个map，key为数组元素，value为元素位置。遍历数组，判断`map.find(target - nums[i])`是否存在，若存在则返回位置，不存在就把`nums[i]`插入map。最终用时24ms。

```cpp
class Solution {
public:
	vector<int> twoSum(vector<int>& nums, int target) {
		map<int, int> map;
		vector<int> result;
		for (int i = 0; i < nums.size(); i++)
		{
			if (map.find(target - nums[i]) != map.end())
			{
				result = { map[target - nums[i]] - 1, i };
				return result;
			}
			map[nums[i]] = i + 1;
		}
		return result;
	}
};
```
