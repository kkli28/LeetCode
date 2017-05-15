> Description

Given an array of strings, group anagrams together.

For example,

```
given: ["eat", "tea", "tan", "ate", "nat", "bat"], 

Return:
[
  ["ate", "eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```

Note: All inputs will be in lower-case.

> Idea

先复制整个字符串数组，对每个单词的字符进行排序，去除多余的重复单词，即可获得不同种类的单词。将它们
放入 `map<string, int>` 中，其中string代表单词种类，int代表其类别。

将源数组中单词取出，复制一个单词副本并进行排序，从map中获得其类别，则该单词分属该类。

> Solution

```C++
class Solution {
public:
	vector<vector<string>> groupAnagrams(vector<string>& strs) {
        //边界条件
		int size = strs.size();
		if (size == 0) return { {} };
		else if (size == 1) return { strs };

		vector<string> vecs = strs;
		for (auto& v : vecs) sort(v.begin(), v.end());      //对单词字符排序
		sort(vecs.begin(), vecs.end());                     //对所有单词排序

        //去掉重复的类型
		auto iter = unique(vecs.begin(), vecs.end());
		vecs.erase(iter, vecs.end());

        //为每个类型编号
		map<string, int> M;
		int index = 0;
		for (auto& v : vecs) M[v] = index++;
		
        //创建group_size个string数组，并对每个单词进行分类
		int group_size = vecs.size();
		vector<vector<string>> result(group_size);
		for (auto& s : strs) {

            //创建单词副本，对其字符排序，便于从map中获取对应单词的类型号
			string tmp = s;
			sort(tmp.begin(), tmp.end());

            //取得类型号，并放入对应数组中
			int group = M[tmp];
			result[group].push_back(s);
		}
		return result;
	}
};
```
