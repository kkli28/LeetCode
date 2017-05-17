> Description

Given a binary search tree, write a function kthSmallest to find the kth smallest element in it.

Note: 
You may assume k is always valid, 1 ? k ? BST's total elements.

Follow up:
What if the BST is modified (insert/delete operations) often and you need to find the 
kth smallest frequently? How would you optimize the kthSmallest routine?

> Idea

找第K大的元素，因此需要从小到大地访问K个元素，中序遍历满足从小到大遍历的要求。

> Solution

```C++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    int count=0;                //访问元素次数
    int result=INT_MIN;         //结果
    int key=0;                  //就是kthSmallest的参数k，减少inorder函数的一个参数而已

    //中序遍历，即可从小到大搜索
    void inorder(TreeNode* root){
        if(root==nullptr) return;
        inorder(root->left);
        ++count;
        if(count==key){
            result=root->val;
            return;
        }
        inorder(root->right);
    }

    int kthSmallest(TreeNode* root, int k) {
        key=k;
        inorder(root);
        return result;
    }
};
```
