> Description

A peak element is an element that is greater than its neighbors.

Given an input array where `num[i] ≠ num[i+1]`, find a peak element and return its index.

The array may contain multiple peaks, in that case return the index to any one of the peaks is fine.

You may imagine that `num[-1] = num[n] = -∞`.

For example, in array `[1, 2, 3, 1]`, 3 is a peak element and your function should return the index number 2.

Your solution should be in logarithmic complexity.

> Idea

题目要求对数复杂度。解法1是暴力法，时间复杂度 `O(n)`。解法2是二分法，满足要求。

> Solution

解法1：

```C++
class Solution {
public:
	int findPeakElement(vector<int>& nums) {
		int size = nums.size();
		if (size == 0) return -1;
		if (size == 1) return 0;
		if (size == 2) {
			return nums[0] > nums[1] ? 0 : 1;
		}
		if (nums[0] > nums[1]) return 0;
		int i = 1;
		for (; i < size - 1; ++i) {
			if (nums[i] > nums[i - 1] && nums[i] > nums[i + 1]) return i;
		}
		if (nums[i] > nums[i - 1]) return i;
	}
};
```

解法2：

```C++
class Solution {
public:
	int findPeakElement(vector<int>& nums) {
		int size = nums.size();
		if (size == 0) return -1;
		if (size == 1) return 0;
		if (size == 2) {
			return nums[0] > nums[1] ? 0 : 1;
		}
		if (nums[0] > nums[1]) return 0;
		int beg = 0;
		int end = nums.size() - 1;
		int mid;

        //二分法
		while (beg != end) {
			mid = (beg + end) / 2;
			if (nums[mid] > nums[mid + 1]) end = mid;
			else beg = mid + 1;
		}
		return beg;
	}
};
```
