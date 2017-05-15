> Description

Given a sorted array consisting of only integers where every element appears twice except for one element which appears once. Find this single element that appears only once.

```
Example 1:
Input: [1,1,2,3,3,4,4,8,8]
Output: 2

Example 2:
Input: [3,3,7,7,10,11,11]
Output: 10
```
Note: Your solution should run in O(log n) time and O(1) space.

> Idea

题目要求 `O(log n)` 复杂度，则不能用逐个元素二进制异或。采用二分法，可以满足要求。

因为数组已排序，因此所有相同元素必然相邻。

将数组一分为二。
如果左部为偶数，比较末尾元素与右部第一个元素。相等则表示左部除去最后一个元素，元素
个数为奇数，只出现一次的数必然在左部；不相等则表示左部偶数个数全部两两出现，只出现一次的数必然在
右部。

如果左部为奇数，思路类似。通过替换更新左部的起始下标beg，切分位置mid和右部结束下标end，可最终当
beg和end相同时，找到只出现一次的数。

> Solution

```C++
class Solution {
public:
	int singleNonDuplicate(vector<int>& nums) {
		int size = nums.size();
		if (size == 1) return nums[0];

		int beg = 0;
		int end = size - 1;
		while (beg!=end) {
			int mid = (beg + end) / 2;
			if ((mid - beg) % 2) {
				if (nums[mid] == nums[mid + 1]) end = mid - 1;
				else beg = mid + 1;
			}
			else {
				if (nums[mid] == nums[mid + 1]) beg = mid;
				else end = mid;
			}
		}
		return nums[beg];
	}
};
```
