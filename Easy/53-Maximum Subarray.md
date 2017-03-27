> Description

Find the contiguous subarray within an array (containing at least one number) which has the largest sum.

For example, given the array `[-2,1,-3,4,-1,2,1,-5,4]`,
the contiguous subarray `[4,-1,2,1]` has the largest sum = 6.

> 思路

求最大子数组。DSAAC上有讲O(n)的算法。但是不同于DSAAC上，这道题不要求最小为0，因此
需要时刻判断sum是否小于0。

> Solution

```C++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int maxSum=INT_MIN;
        int sum=0;
        int size=nums.size();
        for(int i=0;i<size;++i){
            sum+=nums[i];
            if(sum>maxSum) maxSum=sum;
            if(sum<0) sum=0;
        }
        return maxSum;
    }
};
```
