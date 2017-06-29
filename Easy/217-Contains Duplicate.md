> Description

Given an array of integers, find if the array contains any duplicates. Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.

> Idea

对数组排序后，元素前后比较即可。

> Solution

```C++
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        int size=nums.size();
        if(size==0 || size==1) return false;
        sort(nums.begin(), nums.end());
        for(auto iter=nums.begin();iter!=nums.end()-1;++iter){
            if(*iter==*(iter+1)) return true;
        }
        return false;
    }
};
```
