---
layout: post
title: 设计一个栈，实现push、pop、min操作时间复杂度都为O(1)
category: 数据结构
tags: [stack]
---

题目思路很简单，首先需要设计一个链栈来保证push和pop操作都是O(1)，但是栈只能对栈顶进行操作，所以无法确定栈顶元素是否为最小值。

为了保存当前栈中的最小元素，我们维护一个新的栈，当作一个排序栈，保证栈顶元素始终是最小值。

下面是C++实现的代码：

```cpp
#include<iostream>
using namespace std;

class Stack
{
	typedef struct _stack
	{
		int* pElem;
		int size;
		int top;
		_stack(int n) :size(n)
		{
			top = 0;
			pElem = new int[size];
		}
		~_stack()
		{
			delete[]pElem;
			pElem = NULL;
		}
	}stack;

public:

	Stack(int n) :s(n), minstack(n)
	{
	}

	bool pop(int* e)
	{
		if (s.top == 0)
			return false;
		int value = s.pElem[--s.top];
		if (value == minstack.pElem[minstack.top - 1])
			--minstack.top;

		*e = value;
		return true;
	}

	bool push(int value)
	{
		if (s.top == s.size)
			return false;

		if (minstack.top == 0 || value <= minstack.pElem[minstack.top - 1])
			minstack.pElem[minstack.top++] = value;

		s.pElem[s.top++] = value;
		return true;
	}

	bool min(int *pmin)
	{
		if (minstack.top == 0)
			return false;
		*pmin = minstack.pElem[minstack.top - 1];
		return true;
	}

private:
	stack s;
	stack minstack;

};

int main()
{
	Stack s(5);
	s.push(9);
	s.push(7);
	s.push(10);
	s.push(5);
	s.push(8);
	cout << "9 7 10 5 8" << endl;
	int v;
	while (s.pop(&v))
	{
		cout << "pop " << v << "\t";
		if (s.min(&v))
			cout << "min value: " << v << endl;
		else
			cout << "there is no min value!" << endl;
	}
	return 0;
}
```
