> Description

```
Follow up for "Find Minimum in Rotated Sorted Array":
What if duplicates are allowed?

Would this affect the run-time complexity? How and why?
```

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

`(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2)`.

Find the minimum element.

The array may contain duplicates.

> Idea

为什么是Hard难度？同153一样的解，考虑复杂度，先默认第0个元素为最小，跳过所有升序
（包括相等），如果没有到达末尾，则接下来的一个元素就是最小值。

> Solution

```C++
class Solution {
public:
	int findMin(vector<int>& nums) {
		int min = nums[0];
		auto beg = nums.begin();
		while (beg!=nums.end() && *beg >= min) {
			++beg;
		}
		if (beg != nums.end())
			min = *beg;
		return min;
	}
};
```
