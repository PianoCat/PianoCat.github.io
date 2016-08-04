---
layout: post
title: leetcode-226 Invert Binary Tree
category: 算法
tags: [leetcode, Tree]
---

### leetcode-226 Invert Binary Tree ###

* 题目描述

Invert a binary tree.

```
     4

   /   \

  2     7

 / \   / \

1   3 6   9
```
to

```
    4

  /   \

 7     2

/ \   / \

9   6 3   1
```

* 递归解法

用时3ms。

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        if (root == NULL)
			return NULL;
		TreeNode* temp = root->left;
		root->left = invertTree(root->right);
		root->right = invertTree(temp);

		return root;
    }
};
```

* 非递归解法

类似层次遍历，用时0ms。

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        queue<TreeNode*> q;
		if (root == NULL)
			return root;
		q.push(root);
		while (q.size() > 0){
			TreeNode* temp = q.front();
			q.pop();
			TreeNode* left = temp->left;
			temp->left = temp->right;
			temp->right = left;
			if (temp->left)
				q.push(temp->left);
			if (temp->right)
				q.push(temp->right);
		}
		return root;
    }
};
```
