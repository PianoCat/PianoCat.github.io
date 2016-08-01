---
layout: post
title: leetcode-19 Remove Nth Node From End of List
category: 算法
tags: [leetcode]
---

### leetcode-19 Remove Nth Node From End of List ###

* 题目描述

Given a linked list, remove the nth node from the end of list and return its head.

For example,

```
Given linked list: 1->2->3->4->5, and n = 2.

After removing the second node from the end, the linked list becomes 1->2->3->5.
```

* C++解法

这道题目用快慢指针法来求解，即一个指针指向链表头部，第二个指针指向距离头部n个位置的节点，两个指针一起向后移动。当第二个指针移动到链表尾部的时候，第一个指针刚好是倒数第n个节点的前一个指针。代码如下所示，用时4ms：

```cpp
#include<iostream>
#include<vector>
#include<set>
#include<algorithm>
#include<map>

using namespace std;

struct ListNode {
	int val;
	ListNode *next;
	ListNode(int x) : val(x), next(NULL) {}
};

class Solution {
public:
	ListNode* removeNthFromEnd(ListNode* head, int n) {
		ListNode *res = head;
		ListNode *p1 = head;
		ListNode *p2 = p1;

    //判断只有一个节点的情况
		if (p1->next == NULL)
			return NULL;

    //flag用来指示p2指针有没有被允许移动到链表最后
		int flag = 1;
		for (int i = 0; i < n; ++i){
			if (p2->next == NULL){
				flag = 2;
				break;
			}
			p2 = p2->next;
		}
    //双指针向后移动
		while (p2->next != NULL){
			p1 = p1->next;
			p2 = p2->next;
		}
		if (p1 == res && flag == 2)
			return p1->next;

		else
			p1->next = p1->next->next;

		return res;
	}
};

int main()
{
	Solution solution;
	ListNode node1(1);
	ListNode node2(2);
	ListNode node3(3);
	ListNode node4(4);
	ListNode node5(5);

	node1.next = &node2;
	node2.next = &node3;
	node3.next = &node4;
	node4.next = &node5;

	int n = 2;
	ListNode *res = solution.removeNthFromEnd(&node1, n);

	while (res)
	{
		cout << res->val << endl;
		res = res->next;
	}

	return 0;
}
```
