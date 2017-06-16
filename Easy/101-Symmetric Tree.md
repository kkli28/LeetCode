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

方法1：递归。

方法2：使用队列。

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

//////////////////// same: 递归方法 ////////////////////

//以first和second为根节点的两棵树是否相同
bool same(TreeNode* first, TreeNode* second) {
	if (first == 0 && second == 0) return true;         //两树为空
	if (first == 0 || second == 0) return false;        //某一树为空
	if (first->val != second->val) return false;        //根节点的值不同

    //递归判断
	return same(first->left, second->left) && same(first->right, second->right);
}

//////////////////// same: 队列方法 ////////////////////

//以first和second为根节点的两棵树是否相同
bool same(TreeNode* first, TreeNode* second) {
	queue<TreeNode*> q1({ first });
	queue<TreeNode*> q2({ second });

	//广度优先遍历
	while (!q1.empty()) {
		TreeNode* ptr1 = q1.front();
		TreeNode* ptr2 = q2.front();
		q1.pop();
		q2.pop();
		if (ptr1 == 0 && ptr2 == 0) continue;
		if (ptr1 == 0 || ptr2 == 0) return false;
		if (ptr1->val != ptr2->val) return false;
		q1.push(ptr1->left);
		q1.push(ptr1->right);
		q2.push(ptr2->left);
		q2.push(ptr2->right);
	}
	return true;
}

class Solution {
public:
	bool isSymmetric(TreeNode* root) {
        //边界情况
		if (root == 0) return true;

        //反转右子树
		reverse(root->right);

        //判断左右子树是否完全相同
		//注意！上方有两个same方法，正式使用时需要注释掉某一个
		return same(root->left, root->right);
	}
};
```
