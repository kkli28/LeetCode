> Description

Given a linked list, swap every two adjacent nodes and return its head.

For example,
Given `1->2->3->4`, you should return the list as `2->1->4->3`.

Your algorithm should use only constant space. You may not modify the values in the list, only nodes itself can be changed.

> 思路

因为交换两个节点，需要知道前一个节点，因此附加一个头节点到最开始。三个链表指针l0、l1、l2用来标识
前一个节点，待交换的第一个节点，待交换的第二个节点。

让l1的next指向l2所指节点，再l2指向l1，最后l0指向l2，就完成了反转。让l0指向l1，l1指向l1的next指向的
节点，l2指向l1（已后移）的next指向的节点，则完成了整体后移（下一组待交换节点）。

指针后移的过程中，需要注意，一旦指针为0，则表示元素不足两个，应退出。

头结点需要特殊处理，即使l0的next指向head所指（首节点），但是改变l0的next并不能改变head。因此在一开始需要
手动设置head指向l2。算法首部应排除链表元素不足两个的情况。

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
	ListNode* swapPairs(ListNode* head) {

        //特殊情况
		if (head == 0 || head->next == 0) return head;

        //附加头结点，并初始化三个指针。l0指向前一个节点，l1和l2指向待交换的两个节点
		ListNode* l0 = new ListNode(0);
		l0->next = head;
		ListNode* l1 = head;
		ListNode* l2 = head->next;

        //手动设置head的指向
		head = l2;
		
        //开始循环交换
		while (true) {
			l1->next = l2->next;
			l2->next = l1;
			l0->next = l2;

			l0 = l1;
			l1 = l1->next;
			if(!l1) return head;
			l2 = l1->next;
			if(!l2) return head;
		}
	}
};
```
