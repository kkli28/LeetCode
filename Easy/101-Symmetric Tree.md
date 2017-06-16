> Description

Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

For example, this binary tree [1,2,2,3,4,4,3] is symmetric:

```
    1
   / \
  2   2
 / \ / \
3  4 4  3
But the following [1,2,2,null,3,null,3] is not:
    1
   / \
  2   2
   \   \
   3    3
```

Note: Bonus points if you could solve it both recursively and iteratively.

> Idea

判断一棵树是否对称。若一棵树对称，则根节点的右子树翻转后，会和左子树完全相同。因此可先将
右子树翻转，再与左子树节点一一比较即可。

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

 //翻转以root为根的树
void reverse(TreeNode* root) {
	if (root == 0) return;
	TreeNode* ptr = root->left;
	root->left = root->right;
	root->right = ptr;
	reverse(root->left);
	reverse(root->right);
}

//以first和second为根节点的两棵树是否相同
bool same(TreeNode* first, TreeNode* second) {
	if (first == 0 && second == 0) return true;         //两树为空
	if (first == 0 || second == 0) return false;        //某一树为空
	if (first->val != second->val) return false;        //根节点的值不同

    //递归判断
	return same(first->left, second->left) && same(first->right, second->right);
}

class Solution {
public:
	bool isSymmetric(TreeNode* root) {
        //边界情况
		if (root == 0) return true;

        //反转右子树
		reverse(root->right);

        //判断左右子树是否完全相同
		return same(root->left, root->right);
	}
};
```
