> Description

Given an integer (signed 32 bits), write a function to check whether it is a power of 4.

Example:
Given num = 16, return true. Given num = 5, return false.

Follow up: Could you solve it without loops/recursion?

> Idea

```
4^0 -> 1    ->       1
4^1 -> 4    ->     100
4^2 -> 16   ->   10000
4^3 -> 64   -> 1000000
所奇数位上的二进制为1，则满足条件
```

> Solution

循环版本

```C++
class Solution {
public:
    bool isPowerOfFour(int num) {
        if(num==1) return true;
        if(num<4) return false;
        if(num%4) return false;
        int bit=1;
        bool get=false;
        int i=2;
        for(;i<=31;++i){
            int temp=num>>i;
            temp&=bit;
            if(temp==1) {
                if(i%2) return false;
                if(get) return false;
                get=true;
            }
        }
        return true;
    }
};
```

非循环版本：懒得想
