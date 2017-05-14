> Description

Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

> idea

使用递归，分别取得左右子树的最小深度，则父节点的最小深度即左右子树最小深度加1。

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
	int minDepth(TreeNode* root) {
		if (root == nullptr) return 0;
		int depth1 = minDepth(root->left);
		int depth2 = minDepth(root->right);
		int ret=0;
		if(depth1==0) ret=depth2;
		else if(depth2==0) ret=depth1;
		else ret=depth1<depth2?depth1:depth2;
		return 1 + ret;
	}
};
```
