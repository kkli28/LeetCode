> Description

Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

> idea

将每个链表的首元素比较，并将链表指针result指向最小的元素，对应的链表首指针后移，完成初始化。

然后再逐次比较每个链表首指针对应的元素，将最小者添加到result中，对应链表首指针后移。直到只剩
一个非空链表，则直接添加到result最末尾，并返回result。

> Solution

```C++
class Solution {
public:
	ListNode* mergeKLists(vector<ListNode*>& lists) {
		int size = lists.size();

		//特殊情况
		if (size == 0) return 0;
		if (size == 1) return lists[0];


		//处理结果链表首元素
		ListNode* result = 0;
		int minVal = INT_MAX;
		int minIndex = INT_MAX;

		for (int i = 0; i < size; ++i) {
			if (lists[i] && lists[i]->val < minVal) {
				minVal = lists[i]->val;
				minIndex = i;
			}
		}
		if (minIndex == INT_MAX) return 0;
		result = lists[minIndex];
		lists[minIndex] = lists[minIndex]->next;

		//处理剩余元素
		ListNode* temp = result;
		int left = size;			//记录还有多少非空链表
		while (true) {
			minVal = INT_MAX;
			minIndex = INT_MAX;
			for (int i = 0; i < size; ++i) {
				if (lists[i]) {
					if (lists[i]->val < minVal) {
						minVal = lists[i]->val;
						minIndex = i;
					}
				}
				else --left;
			}
			if (left == 0) break;	//全部为空就结束
			else if (left == 1) {	//剩余一个非空，则直接添加到末尾，并结束
				temp->next = lists[minIndex];
				return result;
			}
			else left = size;
			temp->next = lists[minIndex];
			lists[minIndex] = lists[minIndex]->next;
			temp = temp->next;
		}
		return result;
	}
};
```
