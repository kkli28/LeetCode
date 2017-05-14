> Description

Given an input string, reverse the string word by word.

```
For example,
Given s = "the sky is blue",
return "blue is sky the".
```

> idea

将字符串从头到尾分解为逐个单词，并存入双向链表中。最后将链表从尾到首建立
字符串，每个单词间添加一个空格。

> Solution

```C++
class Solution {
public:
	void reverseWords(string &s) {
		auto iter1 = s.begin();             //单词开始标志
		auto end_iter = s.end();            //结束标志
		while (iter1!=end_iter && *iter1 == ' ') ++iter1;
		if (iter1 == end_iter) {
		    s="";
		    return;
		}
		list<string> lst;
		auto iter2 = iter1;                 //单词结束标志
		while (iter1 != end_iter) {
			while (iter2 != end_iter && *iter2 != ' ') ++iter2;     //更新单词结束标志
			lst.push_back(string(iter1, iter2));    //添加单词
			while(*iter2==' ') ++iter2;             //跳过后面的空格
			iter1 = iter2;                          //更新单词开始标志
		}
		auto iter = lst.rbegin();
		s = *iter;                          //用最后一个单词初始化s
		++iter;

        //每个单词间隔一个空格
		for (; iter != lst.rend(); ++iter) s += ' ' + *iter;
	}
};
```
