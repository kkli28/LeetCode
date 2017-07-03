> Description

Given a pattern and a string str, find if str follows the same pattern.

Here follow means a full match, such that there is a bijection between a letter in pattern and a non-empty word in str.

```
Examples:
pattern = "abba", str = "dog cat cat dog"  should return true.
pattern = "abba", str = "dog cat cat fish" should return false.
pattern = "aaaa", str = "dog cat cat dog"  should return false.
pattern = "abba", str = "dog dog dog dog"  should return false.
```

Notes:
You may assume pattern contains only lowercase letters, and str contains lowercase letters separated by a single space.

> Idea

有点麻烦，需要先切词，然后再比较。

比较时，需要pattern中不同的字符对应str中不同的单词，因此需要将pattern中字符
编号，str中字符串也需要编号。不同的字符（串）编号递增，否则编号相同。如若 `aba`，则编号
为121。

例如：
```
pattern: abab       str: pig dog pig dog
pattern编号为1212，str编号为1212，因此为true
```

使用两个vector存储键值对 <int, char> 和 <int, string>即可。
上例中，会导致两个vector为：
```
char_map: <1,a> <2,b> <1,a> <2,b>
str_map : <1,pig> <2,dog> <1,pig> <2,dog>
```
因为两个vector的元素的int域都对应相同，因此为true。

注意！如果只是使用map来建立映射，如pattern中的一个字符与str中一个字符串 <a,pig>，则
无法轻易判断不同字符下的相同字符串，如 <a,pig> 与 <b,pig>。需要遍历整个map，非常麻烦。
因此采用编号的方法。先分别编号，再判断。

> Solution

```C++
//切单词
vector<string> func(const string& str) {
	auto beg = str.begin();
	auto iter = beg;
	auto end = str.end();
	vector<string> vec;
	while (iter != end) {
		if (*iter == ' ') {
			vec.push_back(std::move(string(beg, iter)));
			beg = iter + 1;
		}
		++iter;
	}
	if (beg != iter) vec.push_back(std::move(string(beg, iter)));
	return std::move(vec);
}

class Solution {
public:
	bool wordPattern(string pattern, string str) {
		multimap<char, string> mp;
		int psize = pattern.size();
		vector<string> strs = func(str);
		int ssize = strs.size();

		if (psize != ssize) return false;

		vector<pair<int, char>> char_map;
		vector<pair<int, string>> str_map;

        //初始化char_map
		int index = 0;
		int pindex = 0;
		while (pindex != psize) {
			bool find = false;
			int val = 0;
			int size = char_map.size();
			for (int i = 0; i < size; ++i) {
				if (char_map[i].second == pattern[pindex]) {
					find = true;
					val = char_map[i].first;
					break;
				}
			}
			if (find) {
				char_map.push_back(make_pair(val, pattern[pindex]));
			}
			else char_map.push_back(make_pair(++index, pattern[pindex]));
			++pindex;
		}

        //初始化str_map
		index = 0;
		int sindex = 0;
		while (sindex != ssize) {
			bool find = false;
			int val = 0;
			int size = str_map.size();
			for (int i = 0; i < size; ++i) {
				if (str_map[i].second == strs[sindex]) {
					find = true;
					val = str_map[i].first;
					break;
				}
			}
			if (find) {
				str_map.push_back(make_pair(val, strs[sindex]));
			}
			else str_map.push_back(make_pair(++index, strs[sindex]));
			++sindex;
		}

        //比较两者
		int char_size = char_map.size();
		for (int i = 0; i < char_size; ++i) {
			if (char_map[i].first != str_map[i].first) return false;
		}
		return true;
	}
};
```
