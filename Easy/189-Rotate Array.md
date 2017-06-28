> Description

Rotate an array of n elements to the right by k steps.

For example, with `n = 7` and `k = 3`, the array `[1,2,3,4,5,6,7]` is rotated to 
`[5,6,7,1,2,3,4]`.

Note:
Try to come up as many solutions as you can, there are at least 3 different ways to solve this problem.

> Idea

题目提示至少有三种解法。

解法1：暴力法。将原vector分解成两个vector，原vector再通过两个vector交换位置重组获得。
完全不考虑空间效率，时间效率为 `O(n)`。

解法2：暴力法。将原vector中元素循环右移k%vector.size()次。时间效率为 `O(n*k)`。
超时了，所以不上代码。

解法3：有点麻烦，参见网络上的方法。（叙述不清见谅）
将整个数组分成两部分，即首部移到尾部的部分，和尾部移到首部的部分。通过三个指针
beg，rot和end分隔。beg指示第一部分首，rot指示第二部分首，end指示第二部分尾后。若rot-beg
=m >= end-rot=k，则将首部的前k个元素与尾部交换，并将beg加k，即更改了第一部分的首部位置。
若m < k，则交换首部和尾部的后m个元素，并且end减m，即更改了第二部分的尾部。
整个过程即将需要处理的数组逐渐缩小，最终为0则返回。

> Solution

解法1

```C++
class Solution {
public:
	void rotate(vector<int>& nums, int k) {
		if (nums.size() == 0 || nums.size() == 1) return;
		k = k%nums.size();
		vector<int> nums1{ nums.begin(),nums.end() - k };
		vector<int> nums2{ nums.end() - k,nums.end() };
		nums = nums2;
		for (auto n : nums1) nums.push_back(n);
	}
};
```

解法2：超时了。循环右移k%nums.size()次。

解法3：

```C++
//交换[iter1, iter1+k)与[iter2,iter2+k)的内容
void swap_vec(vector<int>::iterator iter1, vector<int>::iterator iter2, int k) {
	for (int i = 0; i < k; ++i) {
		int num = *iter1;
		*iter1 = *iter2;
		*iter2 = num;
		++iter1;
		++iter2;
	}
}

class Solution {
public:
	void rotate(vector<int>& nums, int k) {
		if (nums.size() == 0 || nums.size() == 1) return;
		k = k%nums.size();
		if(k==0) return;
		auto beg = nums.begin();
		auto rot = nums.end() - k;
		auto end = nums.end();
		while (beg != rot) {
			//更新m和k
			int m = rot - beg;
			k = end - rot;
			if (m >= k) {
				swap_vec(beg, rot, k);
				beg += k;
			}
			else {
				swap_vec(beg, end - m, m);
				end -= m;
			}
		}
	}
};
```
