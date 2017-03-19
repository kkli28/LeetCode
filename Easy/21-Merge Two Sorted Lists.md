> Description

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

> 思路

直接使用两个链表的节点，将它们串联起来即可。故可用一个节点指针result保存第一个元素
较小的链表的首指针，然后用temp指针指示当前已串联的链表的末尾，被指向的指针（l1或l2）
对应后移。（刚开始result为l1或l2，此时已串联1个节点，temp与result同值）。l1和l2比较
它们当前指向的节点，将小的节点串联到result后面（temp指示），然后l1或l2再次后移。直到
一个表为空，则另一个表直接串联到temp所指节点后面。

注意，为了避免特殊情况的干扰，在算法首部需要将特殊情况排除。

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
	ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
		if (l1 == 0) return l2;
		if (l2 == 0) return l1;
		ListNode* result = 0;           //保存结果
		if (l1->val <= l2->val) {
			result = l1;
			l1 = l1->next;
		}
		else {
			result = l2;
			l2 = l2->next;
		}

		ListNode* temp = result;        //下一个节点需要安放的位置
		while (l1 && l2) {
			if (l1->val <= l2->val) {
				temp->next = l1;
				l1 = l1->next;
			}
			else {
				temp->next = l2;
				l2 = l2->next;
			}
			temp = temp->next;
		}

		if (l1) temp->next = l1;        //一个表已消耗完毕，将另一个表直接安放到最后
		else temp->next = l2;
		return result;
	}
};
```