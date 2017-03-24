> Description

Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You may assume no duplicates in the array.

```
Here are few examples.
[1,3,5,6], 5 → 2
[1,3,5,6], 2 → 1
[1,3,5,6], 7 → 4
[1,3,5,6], 0 → 0
```

> 思路

二分查找

> Solution

```C++
class Solution {
public:
	int searchInsert(vector<int>& nums, int target) {
		int size = nums.size();
		int beg = 0;
		int end = size - 1;
		int mid;
		while (beg <= end) {
			mid = (beg + end) / 2;
			if (nums[mid] == target) return mid;
			else if (nums[mid] > target) end = mid - 1;
			else beg = mid + 1;
		}
		return beg;
	}
};
```
