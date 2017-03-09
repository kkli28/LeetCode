> Description

Write a function to find the longest common prefix string amongst an array of strings.

> 思路

排除特殊情况、记录前缀长度，一个一个试呗。

> Solution

```
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        int size=strs.size();

        //排除特殊情况
        if(size==0) return "";
        else if(size==1) return strs[0];
        
        //获取最小字符串长度
        int min_size=INT_MAX;
        for(auto& s: strs) if(s.size()<min_size) min_size=s.size();
        
        char c;
        int count=0;            //记录前缀长度
        bool brk=false;
        for(int i=0;i<min_size;++i){

            //以strs[0]为准
            c=strs[0][i];
            for(auto& s: strs){
                if(s[i]!=c){
                    brk=true;
                    break;
                }
            }
            if(brk) break;
            ++count;
        }
        
        return strs[0].substr(0,count);
    }
};
```
