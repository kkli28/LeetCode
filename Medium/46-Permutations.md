> Description

Given a collection of distinct numbers, return all possible permutations.

```
For example,
[1,2,3] have the following permutations:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

> Idea

循环递归穷举法。大致过程如下（对齐的列表示处于同一个循环）：

```
test case: 1 2 3

    //select a: b c 表示从a b c中，选择a，并且留下b和c供下一次递归选择
    select 1: 2 3       prev: 1         next: 2 3
        select 2: 3     prev: 1 2       next: 3
            select 3:   prev: 1 2 3     next:           solution [1 2 3]
        select 3: 2     prev: 1 3       next: 3
            select 2:   prev: 1 3 2     next:           solution [1 3 2]
    select 2: 1 3
        select 1: 3     prev: 2 1       next: 3
            select 3:   prev: 2 1 3     next:           solution [2 1 3]
        select 3: 1     prev: 2 3       next: 1
            select 1:   prev: 2 3 1     next:           solution [2 3 1]
    select 3: 1 2
        select 1: 2     prev: 3 1       next: 2
            select 2:   prev: 3 1 2     next:           solution [3 1 2]
        select 2: 1     prev: 3 2       next: 1
            select 1:   prev: 3 2 1     next:           solution [3 2 1]
```

> Solution

```C++
class Solution {
public:

    //用于存放结果
	vector<vector<int>> vecs;

    //自己写的递归函数
	void func(vector<int> prev, vector<int> next) {
		int size = next.size();

        //递归结束条件
		if (size == 1) {
			prev.push_back(next[0]);
			vecs.push_back(prev);
			return;
		}

        //循环递归
		for (int i = 0; i < size; ++i) {
			vector<int> vec1 = prev;        //第一个参数
			vec1.push_back(next[i]);        //选择元素

			vector<int> vec_tmp = next;     //第二个参数
			int temp = vec_tmp[0];          //将已被选择的元素移到首部
			vec_tmp[0] = vec_tmp[i];
			vec_tmp[i] = temp;

            //递归调用，第一个参数包含了之前的选择，以及本次的选择（最末尾），
            //第二个参数则为next参数中除去本次所选元素的所有剩余元素
			func(vec1, vector<int>(vec_tmp.begin() + 1, vec_tmp.end()));
		}
	}

    //题目给的函数
	vector<vector<int>> permute(vector<int>& nums) {
		int size = nums.size();

        //边界情况
		if (size == 0) return { {} };
		if (size == 1) return { nums };

        //开始解题
		func(vector<int>(), nums);
		return vecs;
	}
};
```
