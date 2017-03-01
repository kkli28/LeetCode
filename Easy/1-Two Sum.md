> Description

Given an array of integers, return indices of the two numbers such that they add up to a specific target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:
Given nums = [2, 7, 11, 15], target = 9,
Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].

> Solution

```C++
class Solution{
public:
    vector<int> twoSum(vector<int>& nums,int target){
        auto endIter=nums.end();
        auto begIter=nums.begin();
        int value=0;
        int index1=0;
        int index2=0;
        while(begIter!=endIter){
            value=*begIter;
            index2=index1+1;
            for(auto iter=begIter+1;iter!=endIter;++iter){
                if(value+*iter==target) return {index1,index2};
                ++index2;
            }
            ++begIter;
            ++index1;
        }
        return {};
    }
};
```
