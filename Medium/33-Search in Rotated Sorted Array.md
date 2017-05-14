> Description

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.
`(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2)`.
You are given a target value to search. If found in the array return its index, otherwise return -1.
You may assume no duplicate exists in the array.

> idea

找到排序数组向后平移n个元素后中的target位置。一般思路为直接遍历整个容器，但是效率不高。

因为容器已排序，故有两种情况：分成前后两段，每段都已排序（从小到大）；容器刚好因为平移回到有序。

因此如果首元素大于target，则需要找到后半段（如果有）。如果首元素小于target，则只找前半段。

> Solution

```C++
class Solution {
public:
	int search(vector<int>& nums, int target) {
		int size = nums.size();
		if (size == 0) return -1;
		else if (size == 1) {
			if (nums[0] == target) return 0;
			else return -1;
		}

		int index = 0;
		int value = nums[index];

        //首元素大于target时，跳过前半段
		while (value > target) {
			++index;
			if (index == size) return -1;
			value = nums[index];
		}

        //首元素小于target，或后半段开始
		while (value < target) {
			++index;
			if (index == size) return -1;
			value = nums[index];
		}

		if (value == target) return index;
		else return -1;
	}
};
```
