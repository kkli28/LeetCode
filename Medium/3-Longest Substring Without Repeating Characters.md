> Description

Given a string, find the length of the longest substring without repeating characters.

Examples:
Given "abcabcbb", the answer is "abc", which the length is 3.
Given "bbbbb", the answer is "b", with the length of 1.
Given "pwwkew", the answer is "wke", with the length of 3. Note that the answer must 
be a substring, "pwke" is a subsequence and not a substring.

> idea

用begIndex迭代器指向当前找到的最大子串的首部，再用iter从begIndex到末尾，逐个字符
与 `[begIndex,iter)` 中的元素进行比较（使用标准库find）。

如果在 `[begIndex,iter)` 中没有找到 `*iter` 字符，则 `count++` ，并用maxCount记录最大的count。
如果找到了字符，则find返回的迭代器result就指向 `[begIndex,iter)` 中值为 `*iter` 的字符。

begIndex=result+1; 即跳过值为 `*iter` 的字符（因为iter所指就是），此时 `[begIndex,iter)`
中的所有字符均不相等。

> Solution

```C++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        auto begIter=s.begin();
        auto endIter=s.end();
        if(begIter==endIter) return 0;
        int count=0;
        int maxCount=0;
        for(auto iter=begIter;iter!=endIter;++iter){
            auto result=find(begIter,iter,*iter);
            if(result==iter){
                ++count;
                if(count>maxCount) maxCount=count;
            }
            else{
                begIter=result+1;
                count=iter-begIter+1;
            }
        }
        return maxCount;
    }
};
```
