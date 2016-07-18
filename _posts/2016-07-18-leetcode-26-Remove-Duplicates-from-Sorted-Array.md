---
layout: post
title: Remove Duplicates from Sorted Array
category: 算法
tags: [leetcode]
---

### leetcode 26 Remove Duplicates from Sorted Array ###

* 题目描述

Given a sorted array, remove the duplicates in place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this in place with constant memory.

For example,

Given input array nums = `[1, 1, 2]`

Your function should return length = `2`, with the first two elements of nums being `1` and `2` respectively. It doesn't matter what you leave beyond the new length.

+ C++解法一

使用vector中的迭代器来实现,用时60ms。

```cpp

class Solution
{
public:

	int removeDuplicates(vector<int>& nums){
		if (nums.size() < 1)
			return 0;
		int flag = 0;
		for (vector<int>::iterator i = nums.begin()+1; i != nums.end();){

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

};

```
- C++解法二

将vector中数据放入set，利用set不重复不排序的特性，直接输出个数。这种方法用时64ms。

```cpp
class Solution
{
public:

	int removeDuplicates(vector<int>& nums){
		set<int> num_set;
		for (int i = 0;i<nums.size();++i){
			num_set.insert(nums[i]);
		}
		nums.clear();
		for (set<int>::iterator ite = num_set.begin(); ite != num_set.end(); ++ite){
			nums.push_back(*ite);
		}
		return nums.size();
	}

};
```

---
做这道题目的过程中学习到了以下三点：
1. 看清楚题目再做，刚开始没看到标题中的*sorted array*,导致程序写的复杂了。

2. set与vector的不同之处在于set中数据不重复、不排序，直接可以去掉重复的数字。

3. `vector`中的`erase`方法使用必须注意，在`vector.erase(ite)`后ite变成了野指针，所以一般用`ite = vector.erase(ite)`的方法来解决。
