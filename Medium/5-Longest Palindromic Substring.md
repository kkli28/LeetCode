> Description

Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.

Example:
```
Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.
```

Example:
```
Input: "cbbd"
Output: "bb"
```

> 思路

求解字符串中的最长回文字符串，可分两部分进行。第一次扫描类似 `aba` 的字符串，
第二次扫描类似 `abba` 的字符串。效率不高，两次 `O(n^2)` 的操作。

1. 类似于 `aba` 的，下标范围 `i: [0,size-1)`，用内循环 `j:[1,size-1)` 比较当前字符
前j位置和后j位置的元素，一旦不同就退出内循环。相同则计数加2并与保存的最大值相比较。

2. 类似于 `abba` 的，原理同上，但是每次都先判断 `str[i]==str[i+1]?`，如果是则增加
计数并用内层循环分别判断 `str[i]` 前j个位置和 `str[i+1]` 后j个位置。一旦不同就退出循环。

通过两次 `n^2` 的循环（一次判断 `aba` 类型，一次判断 `abba` 类型），即可算出其中的最长串。

> Solution

```C++
class Solution {
public:
    string longestPalindrome(string s) {
        int maxCount=1;
        int count=0;
        int begIndex=0;
        int size=s.size();

        //找aba类型
        for(int i=0;i<size;++i){
            count=1;
            int j=1;
            for(;j<size;++j){
                if(i-j>=0 && i+j<size && s[i-j]==s[i+j]){
                    count+=2;
                    if(count>maxCount){
                        maxCount=count;

                        //begIndex从i-j开始
                        begIndex=i-j;
                    }
                }else break;
            }
        }
        
        //找abba类型
        for(int i=0;i<size;++i){
            count=1;

            //str[i]和str[i+1]必须相同才继续判断
            if(i+1<size && s[i]==s[i+1]){
                ++count;
                if(count>maxCount){
                    maxCount=count;
                    begIndex=i;
                }
                
                int j=1;
                for(;j<size;++j){

                    //注意！需要跳过str[i+1]，即str[i-j]==str[i+j+1]
                    if(i-j>=0 && i+j+1<size && s[i-j]==s[i+j+1]){
                        count+=2;
                        if(count>maxCount){
                            maxCount=count;

                            //begIndex从i-j开始
                            begIndex=i-j;
                        }
                    }
                    else break;
                }
            }
        }

        //返回str中从begIndex开始的maxCount个字符
        return s.substr(begIndex,maxCount);
    }
};
```
