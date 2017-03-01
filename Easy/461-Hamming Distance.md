> Description

The Hamming distance between two integers is the number of positions at 
which the corresponding bits are different.Given two integers x and y, 
calculate the Hamming distance.

Note:
0 ≤ x, y < 231.

Example:
```
Input: x = 1, y = 4
Output: 2
Explanation:
1   (0 0 0 1)
4   (0 1 0 0)
       ↑   ↑
```
The above arrows point to positions where the corresponding bits are different.

> 思路

求出两个整数的汉明距离，即两者二进制表示中对应位不相同的个数。

使用unsigned类型的 `1u` 分别进行0到31次左移，再求非，与两个数或运算，可求出两数对应
位置上二进制位的值。两个结果进行亦或运算，为真就代表一个不相同的位置。

> Solution

```C++
class Solution {
public:
    int hammingDistance(int x, int y) {
        int count=0;
        for(int i=0;i<32;++i){
            if(((~(1u<<i))|x) ^ ((~(1u<<i))|y)) ++count;
        }
        return count;
    }
};
```
