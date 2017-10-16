> Description

Given an array of integers and an integer k, find out whether there are two distinct indices i and j in the array such that nums[i] = nums[j] and the absolute difference between i and j is at most k.

> Idea

用multimap存储 `<值,位置>` ，值自动在multimap中的相邻位置，对相同的值进行值得穷举比较，若
之间的距离小于等于k，则满足条件。若所有都不满足条件，则false。

> Solution

```C++
class Solution {
public:
	bool containsNearbyDuplicate(vector<int>& nums, int k) {
		if (nums.size() < 2) return false;  //特殊条件

        //将<值,位置>装入multimap中
		multimap<int, int> map;
		int size = nums.size();
		for (int i = 0; i < size; ++i) map.insert(make_pair(nums[i], i));
		
        //开始遍历所有值相同的局部
		auto iter1 = map.begin();
		auto iter2 = map.upper_bound(iter1->first);

		auto end = map.end();
		while (iter1 != end) {

            //i1属于[iter1, iter2)
			auto prevIter2 = std::prev(iter2);
			for (auto i1 = iter1; i1 != prevIter2; ++i1) {

                //i2属于(i1, iter2]
				for (auto i2 = std::next(i1); i2 != iter2; ++i2) {
					if (std::abs((i1->second) - (i2->second)) <= k) {
						return true;
					}
				}
			}
			iter1 = iter2;
			if (iter1 == end) return false;     //iter1到结尾，则结束
			iter2 = map.upper_bound(iter1->first);
		}
		return false;
	}
};
```
