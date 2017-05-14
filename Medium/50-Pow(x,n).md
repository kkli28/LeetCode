> Description

Implement pow(x, n).

> idea

快速乘方算法。DSAAC中第24页有介绍。

> Solution

```
class Solution {
public:
    double myPow(double x, int n) {
        if(n<0) return pow(x,n);
        else if(n==0) return 1;
        else if(n==1) return x;
        
        if(n%2) return myPow(x*x,n/2)*x;
        else return myPow(x*x,n/2);
    }
};
```
