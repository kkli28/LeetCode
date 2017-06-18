> Description

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

`(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2)`.

Find the minimum element.

You may assume no duplicate exists in the array.

> Idea

如果完全不考虑性能，则可对整个数组排序，取最小即可。

如果考虑性能，则先默认第0个元素为最小，跳过升序，如果没有到末尾，则下一个元素就是最小值。

> Solution

不考虑任何性能，`O(nlogn)`：

```C++
class Solution {
public:
    int findMin(vector<int>& nums) {
        sort(nums.begin(),nums.end());      //排序取最小
        return nums[0];
    }
};
```

考虑性能，`O(n)`：

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
