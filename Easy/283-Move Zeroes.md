> Description

Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

For example, given nums = [0, 1, 0, 3, 12], after calling your function, nums should be [1, 3, 12, 0, 0].

Note:
You must do this in-place without making a copy of the array.
Minimize the total number of operations.

> Idea

使用两个迭代器分别标识0和1，并当0在前时，交换两者，并更新两者。直到指向0的迭代器
为尾或者尾后即可。

> Solution

```C++
class Solution {
public:
	void moveZeroes(vector<int>& nums) {
        //特殊情况
		if (nums.size() == 0 || nums.size() == 1) return;
		auto z = nums.begin();
		auto nz = nums.begin();
		auto end = nums.end();

		while (true) {

            //找到第一个0
			while (z != end) {
				if (*z == 0) break;
				++z;
			}

            //找到第一个非0
			while (nz != end) {
				if (*nz != 0) break;
				++nz;
			}

			if (z == end-1 || z==end || nz == end) break;

            //非0在0前，则跳过
			if (nz < z) {
				++nz;
				continue;
			}

			//交换两者
			int temp = *z;
			*z = *nz;
			*nz = temp;
		}
	}
};
```
