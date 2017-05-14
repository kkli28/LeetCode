> Description

Given an array of integers sorted in ascending order, find the starting and ending position of a given target value.

Your algorithm's runtime complexity must be in the order of O(log n).

If the target is not found in the array, return [-1, -1].

For example,
Given `[5, 7, 7, 8, 8, 10]` and target value 8,
return `[3, 4]`.

> idea

先判断边界条件，如数组长度为0等。

使用begIndex和endIndex标记开始位置和结束位置。找到target，则begIndex记录开始位置。
endIndex从 `begIndex+1` 位置开始递增，一旦其所标示的位置值不为target，则退出，并
对endIndex减1。将begIndex和endIndex组合并返回。

> Solution

```C++
class Solution {
public:
	vector<int> searchRange(vector<int>& nums, int target) {
		int sz = nums.size();
		if (sz == 0) return{ -1,-1 };
		if (target < nums[0]) return{ -1,-1 };
		if (target > nums[sz - 1]) return{ -1,-1 };

		int begIndex = 0;
		int endIndex = 0;
		for (; begIndex < sz; ++begIndex)
			if (nums[begIndex] == target) break;

		endIndex = begIndex+1;
		if (begIndex == sz) return{ -1,-1 };
		for (; endIndex <sz; ++endIndex)
			if (nums[endIndex] != target) break;
		
		return{ begIndex,endIndex-1 };
	}
};

```