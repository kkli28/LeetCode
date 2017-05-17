> Description

Given an unsorted integer array, find the first missing positive integer.

For example,

```
Given [1,2,0] return 3,
and [3,4,-1,1] return 2.
```

Your algorithm should run in O(n) time and uses constant space.

> Idea

生成一个 `nums.size()+1` 个元素的bool数组，全部取true。将nums中出现元素作为下标设置数组对应元素
为false（下标有效才设置）。然后读数组，一旦遇到true，则返回对应下标。

用 `nums.size()+1` 而非 `nums.size()` 是因为，如果给定的数组为 `[1,2,3]`，则布尔数组需要下标3
有效才能标识元素3的出现，故需要加至少4个元素，因此需要加1。如果元素从1连续出现，则刚好将
布尔数组全部设置为false，此时查找未出现元素的循环（代码中最后一个循环）不能正确return，因此
需要在循环外进行 `return size`。如果一旦有元素没有出现，则布尔数组对应下标的元素为true，查找
未出现元素的循环能正确返回。

> Solution

```C++
class Solution {
public:
    int firstMissingPositive(vector<int>& nums) {
        int size=nums.size();
        if(size==0) return 1;
        ++size;
        bool* arr=new bool[size];
        for(int i=0;i<size;++i) arr[i]=true;
        for(int i=0;i<size;++i){
            if(nums[i]>0 && nums[i]<size) arr[nums[i]]=false;
        }
        for(int i=1;i<size;++i)
            if(arr[i]) return i;
        return size;
    }
};
```
