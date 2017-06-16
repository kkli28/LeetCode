> Description

Given a singly linked list `L: L0→L1→…→Ln-1→Ln`,
reorder it to: `L0→Ln→L1→Ln-1→L2→Ln-2→…`

You must do this in-place without altering the nodes' values.

For example,
Given `{1,2,3,4}`, reorder it to `{1,4,2,3}`.

> Idea

可以为了避免多次循环遍历链表，可以将所有节点的指针用 `vector` 存储。因为是前后对应相连，
因此可以将链表指针组成的数组分成前后两部分，以前部分为基础，后部分各个分别连到前部分
对应位置后面，并设置其后续。即 `vec[0]` 连接 `vec[size-1]`，并将 `vec[size-1]`
连接到 `vec[1]`，即可保证链表的完整性。最后设置 `vec[size/2]` 连接到 `null` 即可，
因为其为最后一个元素。

无论链表个数是偶数还是奇数，链表最后一个元素都是 `vec[size/2]`。举例说明：

```
{1,2,3,4,5}，处理后为 {1,5,2,4,3}，则:
第一次1连5，5连2，即 vec[0] 连接 vec[4]，vec[4]连接 vec[1]，得 1 --> 5--> 2--> 3--> 4 --> 5。
注意，此时4还连着5，即 vec[3] 还连着 vec[4]。因为原本4连着5，而第一次处理后，1连5，
并没有切断4连5，5连3也没有切断4连5，因此4依旧连着5。下一次会自动切断。有点绕，请自行草稿。

第二次2连4，4连3，即 vec[1] 连接 vec[3]，vec[2]，得 1 --> 5--> 2--> 4--> 3 --> 4。
注意，由于4连3，则4不再连着5。而此时3还连着4，即 vec[2] 还连着 vec[3]。

最后设置3的后续为 null，即设置 vec[size/2]==vec[2]的后续为null。切断了3连4。
最终得到 1-->5-->2-->4-->3。

{1,2,3,4,5,6}，处理后为 {1,6,2,5,3,4}，则第一次1连6，6连2。第二次2连5，5连3。
第三次3连4，4连4。最后设置4的后续为 null。
```

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
	void reorderList(ListNode* head) {
        //边界情况
		if (head == 0 || head->next == 0 || head->next->next == 0) return;

        //先将所有节点的指针存储起来
		vector<ListNode*> vec;
		ListNode* p = head;
		while (p) {
			vec.push_back(p);
			p = p->next;
		}

        //第1个连接最后一个，并且最后一个连接第二个。到中间停止
		int size = vec.size();
		for (int i = 0; i < size / 2; ++i) {
			vec[i]->next = vec[size - i - 1];
			vec[size - i - 1]->next = vec[i + 1];
		}

        //设置链表结尾
		vec[size / 2]->next = 0;
	}
};
```
