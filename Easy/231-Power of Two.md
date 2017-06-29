> Description

Given an integer, write a function to determine if it is a power of two.

> Idea

先排除负数，因为2的幂不可能为负。

题目的思路为，若是2的幂，则整个二进制表示中有且只有1位为1，其余都为0。因此可通过
计算数字的二进制表示中1的位数来判断。

解法1：我的解法。循环右移，并判断末尾是否为1。也可通过将1循环左移31次，每次与数字相与来计算。效率不高。

解法2：别人的解法。一行代码实现，即判断 `n&(n-1)==0` 是否成立。若成立，则数字是2的幂。
因为若n的二进制表示中只有1个1，则设其为 `00...00100...00`，则 `n-1` 为
`00...00011...11`，即末尾全部是1，相与后为0。效率很高。

> Solution

解法1：

```C++
class Solution {
public:
	bool isPowerOfTwo(int n) {
	    if(n<1) return false;       //负数
		int count = 0;              //计算n的二进制表示中，1的位数
		for (int i = 0; i < 31; ++i) {
			if (n & 0x1) ++count;
			if (count > 1) return false;
			n >>= 1;
		}
		if (count != 1) return false;
		return true;
	}
};
```

解法2：

```C++
class Solution {
public:
	bool isPowerOfTwo(int n) {
	    return n>0 && !(n&(n-1));
	}
};
```
