> Description

You are given an n x n 2D matrix representing an image.

Rotate the image by 90 degrees (clockwise).

Follow up:
Could you do this in-place?

> Idea

```
1 2 3       7 4 1
4 5 6  -->  8 5 2
7 8 9       9 6 3
```

通过上方示例的矩阵变换，可得知规律，分别从末尾行的第i个元素到
第1行的第i个元素组成一个数组，成为结果的第i行。即末尾行第0个元素7，第二行第0个元素4，第一行的
第0个元素1，组成数组 `7 4 1`，成为结果的第0行。因此可通过两层循环，第一层循环下标（0~n），
第二层（内层）循环行数（末尾到首行）来实现。

> Solution

```C++
class Solution {
public:
	void rotate(vector<vector<int>>& matrix) {
		int size = matrix.size();
		if (size <= 1) return;

		vector<vector<int>> result;
		for (int i = 0; i < size; ++i) {
			vector<int> vec;
			for (int j = size - 1; j >= 0; --j) {
				vec.push_back(matrix[j][i]);
			}
			result.push_back(vec);
		}
		matrix = result;
	}
};
```
