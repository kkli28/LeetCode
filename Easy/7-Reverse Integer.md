> Description

Reverse digits of an integer.

```
Example1: x = 123, return 321
Example2: x = -123, return -321
```

Have you thought about this?
Here are some good questions to ask before coding. Bonus points for you if you have already thought through this!

If the integer's last digit is 0, what should the output be? ie, cases such as 10, 100.

Did you notice that the reversed integer might overflow? Assume the input is a 32-bit integer, then the reverse of 1000000003 overflows. How should you handle such cases?

For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

Note:
The input is assumed to be a 32-bit signed integer. Your function should return 0 when the reversed integer overflows.

> 思路

首先剔除特殊情况，如x为 `INT_MIN` 或 `INT_MAX`。只要不是这两个，必然由负转到正不会溢出。用pos记录x的
符号，并将x转化成正数。然后再转换成字符串（通过取余添加字符的方式，得到的字符串为逆序串，刚好完成了
整数的数字逆转。进行比较时，当字符串长度大于（不可能）等于 `INT_MAX | INT_MIN`，则需要判断该字符串
表示的数是否越界。否则直接将字符串转换成整数，并还原符号。

> Solution

```
class Solution {
public:
	int reverse(int x) {
        //剔除特殊情况
		if (x == INT_MIN || x==INT_MAX) return 0;
		if(x>-10 && x<10) return x;

        //判断正负
		int pos = 0;
		if (x < 0) {
			pos = 1;
			x = -x;
		}

		string str;
		int temp=0; 		//余数
		bool flag=0; 		//标记是否跳过0，一旦有非0值进入str，就不能跳过
		while (x != 0) {
		    temp=x%10;
		    x/=10;
		    if(!flag && temp==0) continue;
			str.push_back(temp + 0x30);
			flag=true; 		//有非0值进入str，标记为不可跳过后续的0
		}

		int result = 0;

		//溢出
		if (str.size()>=10 && str > "2147483647") return 0;
		
		//string转int
		int size = str.size();
		for (int i = 0; i < size; ++i)
			result = result * 10 + str[i] - 0x30;
		return pos?-result:result;
	}
};
```
