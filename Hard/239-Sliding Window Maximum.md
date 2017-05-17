> Description

Given an array nums, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the k numbers in the window. Each time the sliding window moves right by one position.

For example,

```
Given nums = [1,3,-1,-3,5,3,6,7], and k = 3.

Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
Therefore, return the max sliding window as [3,3,5,5,6,7].
```

Note: 
You may assume k is always valid, ie: `1 ≤ k ≤ input array's size` for non-empty array.

Follow up:
Could you solve it in linear time?

> Idea

可以用简单的方法，即循环切k长的段获取最大值（函数调用），放到结果数组中，但是性能比较低，大约
220ms才能跑完测试。因此将函数调用手动内联，并加了条件判断，是否需要循环整个k长度的子串找最大值。

思路为，如果前一次找到的最大值在后一次子串中，则只需比较前一次找到的最大值与最后一个元素即可。因为
当前子串的前 `k-1` 个元素是之前一个子串的 `1~k` 个元素，因此如果前一次的最大值不是第一个元素，则
后一次的子串中，前 `k-1` 个元素的最大值就是该最大值，只需要比较该值与最后一个元素的大小就可找出
最大值。经过优化后，只需要72ms。当然，优化常常伴随着代码的不美观。



> Solution

```C++
class Solution {
public:
	vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        //特殊情况
		if (k == 0) return {};
		if (k == 1) return nums;

        //start指向子数组中的第一个元素，finish指向子数组最后一个元素的后一个元素
		auto start = nums.begin();
		auto finish = start + k;
		auto end = nums.end();
        
		vector<int> result;

        //iter标识最大值所在位置
		auto iter = start;

        //temp_iter用于遍历子数组
		auto temp_iter = start;
		int max = *temp_iter;
		while (++temp_iter != finish) {
			if (*temp_iter > max) {
				iter = temp_iter;
				max = *temp_iter;
			}
		}

		result.push_back(max);
		++start;
		++finish;

        //因为finish指向最后一个元素的后一个元素，因此当finish为end时，
        //[start, finish) 依旧是有效的子数组
		while (finish != end + 1) {

            //若之前的最大值不是第一个元素，则其必然存在于后一个子数组中，只需与末尾元素比较即可
			if (iter != start - 1) {
				if (*(finish - 1) > *iter) {
					iter = finish - 1;
				}
				result.push_back(*iter);
			}

            //之前找到的最大值是第一个元素，则其必然不在后一个子数组中，需要遍历整个子数组
			else {
				temp_iter = start;
				max = *temp_iter;
				iter=temp_iter;         //记住更新iter
				while (++temp_iter != finish) {
					if (*temp_iter > max) {
						iter = temp_iter;
						max = *temp_iter;
					}
				}
				result.push_back(max);
			}
			++start;
			++finish;
		}
		return result;
	}
};
```
