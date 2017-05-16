> Description

Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.

For example,
Given the following matrix:

```
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
```

You should return `[1,2,3,6,9,8,7,4,5]`.

> Idea

顺时针螺旋取数，则可通过四个循环，分别为横向从左到右、竖向从上到下、横向从右到左、竖向从下到上
来完成一个轮回。

再通过四个变量来标识：可取最小行 `min_row`、可取最大行 `max_row`、可取最小列 `min_col`、
可取最大列 `max_col`。四个变量分别初始化为：0、总行数、0、总列数。

当横向从左到右时，分别取 `min_row` 中从 `min_col` 到 `max_col` 中的元素，添加到result中，并
对 `min_row` 递增。

当竖向从上到下时，分别取 `max_col` 中从 `min_row` 到 `max_row` 中的元素，并对 `max_col` 递减。

当横向从右到左时，分别取 `max_row` 中从 `max_col` 到 `min_col` 中的元素，并对 `max_row` 递减。

当竖向从下到上时，分别取 `min_col` 中从 `max_row` 到 `min_row` 中的元素，并对 `min_col` 递增。

每次循环完都判断 `min_row` 是否等于 `max_row` 或 `min_col` 是否等于 `max_col`。如果相等则表示
已取完所有数，则结束。

> Solution

```C++
class Solution {
public:
	vector<int> spiralOrder(vector<vector<int>>& matrix) {
		int row_size = matrix.size();
		if (row_size == 0) return {};
		if (row_size == 1) return matrix[0];

		int col_size = matrix[0].size();
		int min_row = 0;
		int max_row = row_size;
		int min_col = 0;
		int max_col = col_size;
		vector<int> result;
		while (true) {
			for (int i = min_col; i < max_col; ++i) {
				result.push_back(matrix[min_row][i]);
			}
			++min_row;
			if (min_row==max_row) break;
			for (int i = min_row; i < max_row; ++i) {
				result.push_back(matrix[i][max_col-1]);
			}
			--max_col;
			if (min_col==max_col) break;
			for (int i = max_col - 1; i >= min_col; --i) {
				result.push_back(matrix[max_row-1][i]);
			}
			--max_row;
			if (min_row == max_row) break;
			for (int i = max_row - 1; i >= min_row; --i) {
				result.push_back(matrix[i][min_col]);
			}
			++min_col;
			if (min_col == max_col) break;
		}
		return result;
	}
};
```
