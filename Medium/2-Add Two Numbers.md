> Description

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.
You may assume the two numbers do not contain any leading zero, except the number 0 itself.
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8

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
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        int carry=0;
        int value=0;
        int tempValue=0;
        ListNode* retPtr=l1;
        
        ListNode* preL1=l1;
        ListNode* preL2=l2;
        while(l1!=0 && l2!=0){
            value=l1->val+l2->val+carry;
            carry=0;
            if(value>=10){
                tempValue=value%10;
                l1->val=tempValue;
                l2->val-tempValue;
                carry=1;
            }
            else{
                l1->val=value;
                l2->val=value;
            }
            preL1=l1;
            preL2=l2;
            l1=l1->next;
            l2=l2->next;
        }
        if(l1==0){
            preL1->next=l2;
            l1=l2;
        }
        
        while(l1!=0 && carry==1){
            l1->val+=carry;
            carry=0;
            if(l1->val>=10){
                l1->val=l1->val%10;
                carry=1;
                preL1=l1;
                l1=l1->next;
            }
        }
        if(carry==1){
            preL1->next=new ListNode(carry);
        }
        return retPtr;
    }
};
```