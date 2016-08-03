---
layout: post
title: leetcode-110 Balanced Binary Tree
category: 算法
tags: [leetcode, Tree, Depth-first Search]
---

### leetcode-110 Balanced Binary Tree ###

* 题目描述

Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

* C++解法一

最简单暴力的方法，对每一个结点都进行检查，然后递归地去检查其子结点。本方法用时16ms。

```cpp
class Solution {
public:
	bool isBalanced(TreeNode* root) {
		if (root == NULL)
			return true;
		int sub = abs(getHeight(root->left) - getHeight(root->right));
		if (sub > 1)
			return false;
		return isBalanced(root->left) && isBalanced(root->right);

	}

	int getHeight(TreeNode* root){
		if (root == NULL)
			return 0;
		int lh = getHeight(root->left);
		int rh = getHeight(root->right);
		return 1 + (lh > rh ? lh : rh);
	}

};
```

题目做到这里感觉不太甘心，因为肯定有更好的解法，利用更少的时间来解决这个问题。有空研究研究。
