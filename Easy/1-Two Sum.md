> Description

Given an array of integers, return indices of the two numbers such that they add up to a specific target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:
Given nums = [2, 7, 11, 15], target = 9,
Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].

> 思路

从容器中找到两个数的和为目标数target，最简单的方法就是遍历容器咯。为了
效率，将每次内层递增都使用的值 `*begIter` 用变量value存储。

不能通过 `*begIter` 的值大于target就跳过之，因为题目没有说容器中
的数不能为负数。例如 `target==-8` 而 `*begIter==-1` ，如果容器中
有元素 `-7`，则能组成结果（有此测试案例）。所以还是老老实实遍历吧。。。

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
