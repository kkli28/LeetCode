> Description

Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

```
For example:
Given the below binary tree and sum = 22,
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \      \
        7    2      1
```
return true, as there exist a root-to-leaf path 5->4->11->2 which sum is 22.

> idea

通过递归的方式，分别求左右子树的路径和是否等于 `sum- root->val`。

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
	bool pathSum(TreeNode* root, int sum) {
		if (root == nullptr) {
			if (sum == 0) return true;
			else return false;
		}

        //注意，只有当左右子树都为空时，才是叶节点
		if (root->left == nullptr && root->right == nullptr) {
			if (root->val == sum) return true;
			return false;
		}

		if(root->left && root->right)
			return pathSum(root->left, sum - root->val)|| pathSum(root->right, sum - root->val);

		if (root->left) return pathSum(root->left, sum - root->val);
		if (root->right) return pathSum(root->right, sum - root->val);
	}
	bool hasPathSum(TreeNode* root, int sum) {
		if (root == nullptr) return false;
		return pathSum(root, sum);
	}
};
```
