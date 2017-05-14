> Description

Invert a binary tree.

```
     4
   /   \
  2     7
 / \   / \
1   3 6   9
to
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```

> Idea

递归交换左右子树指针即可。

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
    TreeNode* invertTree(TreeNode* root) {
        if(root==nullptr) return root;

        //交换左右子树指针
        TreeNode* ptr=root->left;
        root->left=root->right;
        root->right=ptr;

        //递归翻转左右子树
        invertTree(root->left);
        invertTree(root->right);
        return root;
    }
};
```
