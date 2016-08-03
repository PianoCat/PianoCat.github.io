---
layout: post
title: leetcode-292 Nim Game
category: 算法
tags: [leetcode, Brainteaser]
---

### leetcode-292 Nim Game ###

* 题目描述

You are playing the following Nim Game with your friend: There is a heap of stones on the table, each time one of you take turns to remove 1 to 3 stones. The one who removes the last stone will be the winner. You will take the first turn to remove the stones.

Both of you are very clever and have optimal strategies for the game. Write a function to determine whether you can win the game given the number of stones in the heap.

For example, if there are 4 stones in the heap, then you will never win the game: no matter 1, 2, or 3 stones you remove, the last stone will always be removed by your friend.

* 题目分析与解法

刚看到题目的时候，感觉是可以用递归的思想来解决，但是模拟了几分钟发现不太容易模拟。后来就去找能赢对方的规律，发现石头个数是`1,2,3`的时候都可以赢，`4`的时候肯定不能赢。那么不管是甲还是乙，只要最后剩下4块石头，那他就不可能获胜。因此甲要获胜的话，一定不能给自己留4块石头。。一直推到8块石头的时候，发现其实就是`%4`，如果`=0`，那么就不能获胜。

代码如下，用时0ms。

```cpp
class Solution {
public:
	bool canWinNim(int n) {
		return n % 4;
	}
};
```
