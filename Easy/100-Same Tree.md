> Description

Given two binary trees, write a function to check if they are equal or not.

Two binary trees are considered equal if they are structurally identical and the nodes have the same value.

> idea

先判断两个根节点指针，然后再递归判断左子树和右子树。

> Solution

```C++
class Solution {
public:
	bool isSameTree(TreeNode* p, TreeNode* q) {
		if ((p && (!q)) || (!p && q)) return false;
		if ((!p) && (!q)) return true;
		if (p->val != q->val) return false;

        //递归左右子树
		return isSameTree(p->left, q->left) && isSameTree(p->right, q->right);
	}
};
```
