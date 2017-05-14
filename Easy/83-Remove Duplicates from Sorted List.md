> Description

Given a sorted linked list, delete all duplicates such that each element appear only once.

For example,
Given `1->1->2` , return `1->2` .
Given `1->1->2->3->3` , return `1->2->3` .

> idea

两个指针prePtr和nextPtr，prePtr指向前一个节点，nextPtr指向后一个节点，如果两者指向的节点的值
相同，则prePtr不变，且prePtr的next域指向nextPtr的next域所指节点，否则prePtr后移。nextPtr每次
都后移。

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
    ListNode* deleteDuplicates(ListNode* head) {
        if(head==0 || head->next==0) return head;
        ListNode* prePtr=head;
        ListNode* nextPtr=head;
        nextPtr=nextPtr->next;
        while(nextPtr){
            if(prePtr->val==nextPtr->val){
                prePtr->next=nextPtr->next;
            }
            else{
                prePtr=prePtr->next;
            }
            nextPtr=nextPtr->next;
        }
        return head;
    }
};
```
