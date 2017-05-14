> Description

Given an array of integers, every element appears twice except for one. Find that single one.

Note:
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

> idea

所有数字异或，最后结果就是带求的数。因为除了待求的数，其余都是两个，故
每相同的两个数对应的二进制都是相同，互相异或为0（不论所有这些数的异或顺序）。
单独的一个数最终会保留其二进制形式，也就是其自己。

> Solution

```C++
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int result=0;
        int size=nums.size();
        for(int i=0;i<size;++i)
            result^=nums[i];
        return result;
    }
};
```
