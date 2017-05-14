> Description

Reverse a singly linked list.

A linked list can be reversed either iteratively or recursively. Could you implement both?

> idea

普通解法：
将 list1 从头到尾插入到 list2 的头部，如 `list1: 1 --> 2 --> 3`，首先 1 插入到 list2 首部，得
`list1: 2 --> 3`，`list2: 1`。然后 2 插入到 list2 首部，得 `list1: 3`，`list2: 2 --> 1`。最后
将3插入到 list2 首部，得 `list1: `，`list2: 3 --> 2 --> 1`，最终 list2 即 list1 的反转。

递归解法：
反转链表list，等价于反转节点list（表示头结点）和链表 `list->next`（将节点添加到链表尾，
即节点与链表的反转）。而反转链表list和反转链表
`list->next` 是等价的，因此可用递归来求解。

> Solution

```C++
//普通解法
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
	ListNode* reverseList(ListNode* head) {
		ListNode* list=nullptr;
		while (head) {
			ListNode* ptr = head;
			head = head->next;
			ptr->next = list;
			list = ptr;
		}
		return list;
	}
};

//递归解法
class Solution {
public:
	ListNode* reverseList(ListNode* head) {
		if (head == nullptr || head->next == nullptr) return  head;

        //反转head->next
		ListNode* reverse=reverseList(head->next);

        //保存头结点
		ListNode* ret = reverse;

        //反转head和head->next
		while (reverse->next) reverse = reverse->next;
		reverse->next = head;
		head->next = nullptr;

		return ret;
	}
};
```
