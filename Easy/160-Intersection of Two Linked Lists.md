> Description

Write a program to find the node at which the intersection of two singly linked lists begins.

For example, the following two linked lists:

```
A:          a1 → a2
                   ↘
                     c1 → c2 → c3
                   ↗            
B:     b1 → b2 → b3
begin to intersect at node c1.
```

Notes:

If the two linked lists have no intersection at all, return null.

- The linked lists must retain their original structure after the function returns.
- You may assume there are no cycles anywhere in the entire linked structure.
- Your code should preferably run in O(n) time and use only O(1) memory.

> Idea

题目要求最好 `O(n)` 的时间复杂度，以及 `O(1)` 的空间复杂度。解法1只满足时间复杂度，
没有满足空间复杂度。解法2则满足两者。当然，O(n^2)的解法就无视了。

```
解法1: 时间复杂度O(n)，空间复杂度O(n)
先将两个链表的所有节点指针存储在vector中，然后从后往前比较指针，返回最后一个相同的
指针即可。如果没有则返回0。
```

```
解法2:
先计算两链表的长度。用两个指针指向两个链表，计算长度差，指向长链表的指针后移长度差个位置。
此时两指针指向的链表等长。然后循环比较两指针，如果相等则返回它，否则两者都后移。如果最后
都没有相同，则返回0。
```

> Solution

解法1：

```C++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
	ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
		vector<ListNode*> vec1;
		vector<ListNode*> vec2;

        //构造vec1
		ListNode* ptr = headA;
		while (ptr != 0) {
			vec1.push_back(ptr);
			ptr = ptr->next;
		}
        
        //构造vec2
		ptr = headB;
		while (ptr != 0) {
			vec2.push_back(ptr);
			ptr = ptr->next;
		}

        //用pos标识最前相同指针
		int pos = vec1.size();
		for (int i = vec1.size() - 1, j = vec2.size() - 1; i >= 0 && j >= 0; --i, --j) {
			if (vec1[i] == vec2[j]) {
				pos = i;
			}
			else break;
		}
		if (pos == vec1.size()) return 0;
		else return vec1[pos];
	}
};
```

解法2：

```C++
class Solution {
public:
	ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
		int size1 = 0;
		int size2 = 0;

		//size1
		ListNode* ptr = headA;
		while (ptr != 0) {
			++size1;
			ptr = ptr->next;
		}

		//size2
		ptr = headB;
		while (ptr != 0) {
			++size2;
			ptr = ptr->next;
		}

		//diff
		int diff = size1 - size2;
		if (diff < 0) diff = -diff;
		
		ListNode* ptrA = headA;
		ListNode* ptrB = headB;
		int size = 0;
		if (size1 > size2) {
			size = size2;
			while (diff--) headA = headA->next;
		}
		else {
			size = size1;
			while (diff--) headB = headB->next;
		}
		for (int i = 0; i < size; ++i) {
			if (headA == headB) break;
			else {
				headA = headA->next;
				headB = headB->next;
			}
		}
		return headA;
	}
};
```
