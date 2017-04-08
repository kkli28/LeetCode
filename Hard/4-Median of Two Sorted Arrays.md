> Description

There are two sorted arrays nums1 and nums2 of size m and n respectively.
Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

Example 1:
nums1 = [1, 3]
nums2 = [2]
The median is 2.0

Example 2:
nums1 = [1, 2]
nums2 = [3, 4]
The median is (2 + 3)/2 = 2.5

> 思路

求两个排序容器中元素的中位数。为什么是Hard难度？？？（注意看题，O(log(m+n))复杂度！！！我是智障）
两容器内容按顺序合并，奇数个数则返回中间值，偶数个数则返回中间两个值得平均值。

> Solution

```C++
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        int size=nums1.size()+nums2.size();
        vector<int> nums;
        nums.reserve(size);
        auto iter1=nums1.begin();
        auto iter2=nums2.begin();
        auto endIter1=nums1.end();
        auto endIter2=nums2.end();
        while(true){
            if(iter1!=endIter1 && iter2!=endIter2){
                if(*iter1<*iter2) nums.push_back(*iter1++);
                else nums.push_back(*iter2++);
            }else break;
        }
        if(iter1==endIter1)
            while(iter2!=endIter2) nums.push_back(*iter2++);
        else while(iter1!=endIter1) nums.push_back(*iter1++);
        if(size%2) return nums[size/2];
        else return ((double)(nums[size/2-1]+nums[size/2]))/2;
    }
};
```
