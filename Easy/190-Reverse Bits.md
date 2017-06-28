> Description

Reverse bits of a given 32 bits unsigned integer.

For example, given input `43261596` (represented in binary as `00000010100101000001111010011100`), return `964176192` (represented in binary as `00111001011110000010100101000000`).

Follow up:
If this function is called many times, how would you optimize it?

> Idea

使用标准库bitset容器，将值放入，然后将其转化为string，再对string反转。然后再转入bitset。最后将其转换成数字类型即可。

> Solution

```C++
class Solution {
public:
	uint32_t reverseBits(uint32_t n) {
		bitset<32> bs1(n);
		string str = bs1.to_string('0', '1');
		reverse(str.begin(), str.end());
		bitset<32> bs2(str, 0, 32, '0', '1');
		return bs2.to_ullong();
	}
};
```
