> Description

Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.

```
For example, 
Given [0,1,0,2,1,0,1,3,2,1,2,1], return 6.
```

> Idea

`first_extremum` 存储已找得到的最大极值，`second_extremum` 依次存储找到的极值。比较两个极值，
并将两者之间的小于极值的数与极值的差值累加到结果中，并将该数增加到小的极值。如果 `second_extremum` 是新的最大极值，则更新 `first_extremum`。

例如：

```
height: [0,1,0,2,1,0,1,3,2,1,2,1]

// f_e代表first_extremum，s_e代表second_extremum，
// index1代表first_extremum的下标，index2代表second_extremum的下标

//1
f_e: 0    s_e: 1    index1: 0    index2: 1    smaller: 0
在[0,1]中找小于smaller的数，没有，跳过

//2
f_e: 1    s_e: 2    index1: 1    index2: 3    smaller: 1
在[1,3]中找小于smaller的数，有height[2]==0小于1，故result加1，且height[2]补齐到1，
此时result==1，height: 0 1 1 2 1 0 1 3 2 1 2 1。

//3
f_e: 2    s_e: 3    index1: 3    index2: 7    smaller: 2
在[3,7]中找小于smaller的数，有height[4]==1、height[5]==0、height[6]==1小于3，故
result分别加1、2、1，且height对应的元素补齐到2，此时result==5，
height: 0 1 1 2 2 2 2 3 2 1 2 1

//4
f_e: 3    s_e: 2    index1: 7    index2: 10    smaller: 2
在[7,10]中找小于smaller的数，有height[9]==1，result加上1，height[9]补齐到2，
此时result==6，height: 0 1 1 2 2 2 2 3 2 2 2 1

//5
没有再找到极值，故退出，得结果result==6。

//注意，可能在最后一个元素是极值，但是此时循环会结束而不会进入判断（看下方代码），故需要
在退出循环时再判断index1和index2是否相同，如果不相同，还需要在[index1,index2]中找小于
smaller的数，并将差值累加到result中。
```

> Solution

```C++
class Solution {
public:
	int trap(vector<int>& height) {
		int size = height.size();
		if (size <= 2) return 0;

		//init first_extremum
		int first_index = 0;
		int second_index = 0;
		int first_extremum = height[0];
		int second_extremum = height[0];
		int result = 0;
		bool skip = true;

		for (int i = 1; i < size; ++i) {

			if (skip) { //值下降的阶段
				if (height[i] <= height[i - 1]) continue;
				else {
					second_extremum = height[i];
					second_index = i;

                    //当元素值开始递增，则进入找极值阶段
					skip = false;
				}
			}
			else { //找极值阶段

				if (height[i] <= height[i - 1]) {   //找到极值
					int smaller = first_extremum < second_extremum ?
						first_extremum : second_extremum;

                    //递增result，并补齐height中[first_index, second_index]的数到smaller
					for (int j = first_index+1; j < second_index; ++j) {
						if (height[j] < smaller) {
							result += smaller - height[j];
							height[j] =smaller;
						}
					}

                    //first_extremum存储最大极值
					if (second_extremum > first_extremum) {
						first_extremum = second_extremum;
						first_index = second_index;
					}

                    //默认重新进入元素值下降的阶段
					skip = true;
				}
				else {  //可能后方还有更大的数，即当前数可能不是极值
					second_extremum = height[i];
					second_index = i;
				}
			}
		}
		
        //可能最后一个数是极值，但是循环退出而执行不到处理代码，故需要再这里进行判断
		if (first_index != second_index) {
			int smaller = first_extremum < second_extremum ?
				first_extremum : second_extremum;
			for (int j = first_index + 1; j < second_index; ++j) {
				if (height[j] < smaller) result += smaller - height[j];
			}
		}
		return result;
	}
};
```
