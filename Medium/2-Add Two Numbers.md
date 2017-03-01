> Description

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.
You may assume the two numbers do not contain any leading zero, except the number 0 itself.
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8

> 思路

两个链表的节点值，对应从链表首加到一个链表结束。如果有进位则用carry变量记录并累加到后一个计算中。

所有的计算结果均用于修改第一个链表即 `l1`。此过程中用两个指针preL1和preL2记录两个链表当前相加
节点的上一个节点。为了当某一个链表已到链表尾时，可修改其尾节点的指针域。

当第一个链表较短时，如果此链表为l1，则将l1的尾节点（通过preL1）指针域修改为指向当前第二个链表对应
的位置，并继续累加carry，直到最后。可能最后一个节点为9且carry为1，则需要新建一个节点来存进位。

最后返回l1的首指针（已用retPtr在函数首保存）。

为了效率，即不新建节点存储计算结果，就直接将运算结果存放于第一个链表 l1 中。

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
        ListNode* retPtr=l1;                    //return pointer
        
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

        //attention
        if(carry==1){
            preL1->next=new ListNode(carry);
        }
        return retPtr;
    }
};
```