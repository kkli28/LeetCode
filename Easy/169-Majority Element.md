> Description

Given an array of size n, find the majority element. The majority element is the element that appears more than ⌊ n/2 ⌋ times.

You may assume that the array is non-empty and the majority element always exist in the array.

> Idea

用map存储数以及对应出现的次数。当出现次数大于等于一半时，就返回该数。一半需要向上取整，
如11个数，则一半为6，因为循环中是以 `>=` 判断的。

> Solution

```C++
class Solution {
public:
	int majorityElement(vector<int>& nums) {
		map<int, int> mp;

		int size = nums.size();
		int half_size = size / 2;
		if (size % 2) half_size += 1;

		auto beg = nums.begin();
		auto end = nums.end();
		while (beg != end) {
			++mp[*beg];
			if (mp[*beg] >= half_size) {
				return *beg;
			}
			++beg;
		}
	}
};
```
