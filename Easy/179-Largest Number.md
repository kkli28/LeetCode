> Description

Given a list of non negative integers, arrange them such that they form the largest number.

For example, given `[3, 30, 34, 5, 9]`, the largest formed number is 9534330.

Note: The result may be very large, so you need to return a string instead of an integer.

> Idea

主要是实现元素的排序准则。可通过自己传入sort函数的第三个参数来实现。

我的实现是分别比较传入的两个数对应的string的大小。通过迭代器单个字符比较来判断。
有点麻烦。

下方的代码参考了别人的方式，即若 `s1+s2 > s2+s1`，则s1更“大”，十分简洁。

> Solution

```C++
class Solution {
public:
	string largestNumber(vector<int>& nums) {
        //对数排序
		sort(nums.begin(), nums.end(), [](int n1, int n2) {
			string s1 = to_string(n1);
			string s2 = to_string(n2);
			return s1 + s2 > s2 + s1; });
		string result;
		for (auto n : nums) result += to_string(n);

        //去掉首部的0
		auto beg = result.begin();
		auto end = result.end();
		while (result.size() > 0 && beg != end && *beg == '0') ++beg;
		if (beg == end) return "0";
		return result;
	}
};
```
