> Description

Find the contiguous subarray within an array (containing at least one number) which has the largest product.

For example, given the array `[2,3,-2,4]`,
the contiguous subarray `[2,3]` has the largest product = 6.

> Idea

方法1：穷举。以 `i: [0~size)` 为起始点，`j: [i~size)` 逐个相乘并与max比较，取最大值。

方法2：两次单遍扫描。从前往后扫描，逐个相乘并与max比较。如果结果为负，则可能再次
遇到正数，因此不能直接使用 `《数据结构与算法分析--C语言描述》` 中的变种联机算法，需要
使用一个 `sum_temp` 来记录负数。同时可能需要丢弃第一个负数，如 `[2,-5,-2,-4,3]` ，
如果一边扫描，则结果为20，正确结果是24。因此单遍扫描不能满足要求，需要从后再扫描一次，
比较两次扫描的最大值。（有点玄乎）。

> Solution

穷举法，复杂度 `O(n^2)`。
```C++
class Solution {
public:
	int maxProduct(vector<int>& nums) {
		int sum = 1;
		int size = nums.size();
		if (size == 1) return nums[0];
		int max = nums[0];

        //i作为乘法起始点
		for (int i = 0; i < size; ++i) {
			sum = 1;
            //j从i开始，与后方所有元素逐个相乘，每次都与max比较，max取较大者
			for (int j = i; j < size; ++j) {
				sum *= nums[j];
				if (sum > max) max = sum;
			}
		}
		return max;
	}
};
```

单遍扫描法，复杂度 `O(n)`。
```C++
int func(vector<int>& nums) {
	int sum = 1;
	int sum_temp = 1;
	int size = nums.size();
	if (size == 1) return nums[0];
	int max = nums[0];
	for (int i = 0; i < size; ++i) {
		sum *= nums[i];
		sum_temp *= nums[i];
		if (sum_temp > 0 && sum_temp > sum) {
			sum = sum_temp;
			sum_temp = 1;
		}

		if (sum > max) max=sum;
		if (sum == 0) sum = 1;
		if (sum < 0) {
			sum_temp = sum;
			sum = 1;
		}
	}
	return max;
}

class Solution {
public:
	int maxProduct(vector<int>& nums) {
		int max1 = func(nums);      //获取正序最大值
		reverse(nums.begin(), nums.end());
		int max2 = func(nums);      //获取逆序最大值
		return max1 > max2 ? max1 : max2;
	}
};
```
