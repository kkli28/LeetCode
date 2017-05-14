> Description

Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.

Note:
You may assume that nums1 has enough space (size that is greater or equal to m + n) to hold additional elements from nums2. The number of elements initialized in nums1 and nums2 are m and n respectively.

> idea

从头到尾遍历两个数组，下标均从0开始，将较小的一个放入中间数组中，并递增下标（另一个不递增）。
直到某一个数组全部放入中间数组，另一个则直接放入中间数组即可。

题目要求结果放入第一个参数中，因此用一个中间数组存储结果，再赋值即可。

> Solution

```C++
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        vector<int> vec;
        int i=0;
        int j=0;
        while(i<m && j<n){
            if(nums1[i]<nums2[j]) vec.push_back(nums1[i++]);
            else vec.push_back(nums2[j++]);
        }
        while(i<m) vec.push_back(nums1[i++]);
        while(j<n) vec.push_back(nums2[j++]);
        nums1=vec;
    }
};
```
