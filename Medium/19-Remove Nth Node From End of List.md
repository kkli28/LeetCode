> Description

Given a linked list, remove the nth node from the end of list and return its head.

For example,

```
Given linked list: 1->2->3->4->5, and n = 2.

After removing the second node from the end, the linked list becomes 1->2->3->5.
```

Note:
Given n will always be valid. Try to do this in one pass.

> Idea

先用一个指针ptr指向链表的第n个元素，然后让另一个用于指向删除节点前一个节点的指针node指向head。
当ptr的next域不为nullptr，则两者同时后移。当ptr的next域为nullptr，则删除node所指节点的下一个节点
即可。

> Solution

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
	ListNode* removeNthFromEnd(ListNode* head, int n) {
		ListNode* ptr = head;
		while (n) {
			ptr = ptr->next;
			--n;
		}

        //List刚好只有n个元素，则head后移即可
		if (ptr == nullptr) {
			head = head->next;
			return head;
		}

        //List不至n个元素，则需要node来标识待删除节点的上一个节点
		ListNode* node = head;
		while (ptr->next != nullptr) {
			ptr = ptr->next;
			node = node->next;
		}

        //简单地丢弃节点即可
		node->next = node->next->next;
		return head;
	}
};
```
