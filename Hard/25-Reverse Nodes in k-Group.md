> Description

Given a linked list, reverse the nodes of a linked list k at a time and return its modified list.

k is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of k then left-out nodes in the end should remain as it is.

You may not alter the values in the nodes, only nodes itself may be changed.

Only constant memory is allowed.

```
For example:

Given this linked list: 1->2->3->4->5

For k = 2, you should return: 2->1->4->3->5

For k = 3, you should return: 3->2->1->4->5
```

> 思路

先创建一个附加节点，其next域指向head所指节点。这样就可以用一个逻辑处理所有组。

用k+1个链表指针用于个指向每组（k个元素）的前一个节点，以及该组的所有节点。

例如原本链表：`1 -> 2 -> 3 -> 4 -> 5 -> 6`，则附加节点0，得链表：
`0 -> 1 -> 2 -> 3 -> 4 -> 5 -> 6`，若 `k==4`，则五个指针l0指向0，l1指向1，
l2指向2，l3指向3，l4指向4。

将l1所指的1的next指向l4所指的4的next域所指的节点，即 `0 -> 1 -> 5`，和 
`2 -> 3 -> 4`，然后l4所指的4的next域赋值为l3（指向3），即 `2 -> 3 <- 4`。
再l3所指的3的next域赋值为l2，即 `2 -><- 3 <- 4`，然后l2所指的2的next域赋值为l1，
即 `0 -> 1 ->5` 和 `4 -> 3 -> 2 -> 1`。最终l0赋值为l4，得 
`0 -> 4 -> 3 -> 2 -> 1 -> 5 -> 6`。反转了前四个元素。

移动l0 l1 l2 l3 l4，如果某个为空，则表示后续元素不能组成k个元素的组，则直接退出。
若都不为空，则移动后l0应该指向前一次操作组的最后一个元素。以此类推即可。

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
	ListNode* reverseKGroup(ListNode* head, int k) {
		if (k == 0 || k == 1) return head;
		vector<ListNode*> vec(k + 1, 0);
		
		ListNode* temp = new ListNode(0);
		temp->next = head;
		vec[0] = temp;

		for (int i = 1; i <= k; ++i) {
			if (temp == 0 || temp->next == 0) return head;
			temp = temp->next;
			vec[i] = temp;
		}

		head = vec[k];
		//init ListNode* s
		while (true) {
			vec[0]->next = vec[k];
			vec[1]->next = vec[k]->next;
			for (int i = 2; i <= k; ++i)
				vec[i]->next = vec[i - 1];
			
			vec[0] = vec[1];
			if (vec[1]->next) vec[1] = vec[1]->next;
			else return head;
			for (int i = 2; i <= k; ++i) {
				vec[i] = vec[i - 1]->next;
				if (!vec[i]) return head;
			}
		}
	}
};
```
