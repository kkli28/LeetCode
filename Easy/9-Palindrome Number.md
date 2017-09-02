> Description

Determine whether an integer is a palindrome. Do this without extra space.

click to show spoilers.

Some hints:
Could negative integers be palindromes? (ie, -1)

If you are thinking of converting the integer to string, note the restriction of using extra space.

You could also try reversing an integer. However, if you have solved the problem "Reverse Integer", you know that the reversed integer might overflow. How would you handle such case?

There is a more generic way of solving this problem.

> Idea

判断所给数字是否是回文，负数不算。分别获取数字的首尾位并比较，相同则继续，不同则返回false，然后去掉首尾并继续，直到数字只有一位或零位为止。

> Solution

```C++
class Solution {
public:
	bool isPalindrome(int x) {
		if (x < 0) return false;
		int i = 0;
		int divisor = 1;
		while (true) {
			if (x / divisor < 10) break;
			divisor *= 10;
			++i;
		}
		while (x > 0) {
			if (x / divisor != x % 10) return false;
			x = x%divisor;
			x = x / 10;
			divisor /= 100;
		}
		return true;
	}
};
```
