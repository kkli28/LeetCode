> Solution

Sort a linked list in O(n log n) time using constant space complexity.

> Idea

时间复杂度要求为 `O(nlogn)`，因此不能每次只排一个节点。如何使用快速排序呢？

可以将所有节点的指针存储在一个 `vector` 中，然后对每个节点指针进行排序，自己
写一个函数对象作为排序准则，即比较节点指针所指的值。整个过程忽视节点的 `next` 域。

最后将排序后的节点指针串联起来，即重建节点之间的关系，并返回 `vector` 首元素即可。

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
class cmp {
public:
	bool operator()(ListNode* f, ListNode* s) {
		return f->val < s->val;
	}
};

class Solution {
public:
	ListNode* sortList(ListNode* head) {
        //边界情况
		if (head == 0 || head->next == 0) return head;

        //存储所有节点的指针
		vector<ListNode*> vec;
		while (head) {
			vec.push_back(head);
			head = head->next;
		}
        
        //对节点排序，排序准则为比较节点指针所指的值
		sort(vec.begin(), vec.end(), cmp());

        //重建链表
		int size = vec.size();
		for (int i = 0; i < size-1; ++i) {
			vec[i]->next = vec[i + 1];
		}

        //最后一个元素需要将next域设置为0
		vec[size - 1]->next = 0;
		return vec[0];
	}
};
```
