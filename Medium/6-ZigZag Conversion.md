> Description

The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

```
P   A   H   N
A P L S I I G
Y   I   R
```

And then read line by line: "PAHNAPLSIIGYIR"

> idea

根据规律，可知，n行则可每 `n+n-2==2n-2` 个元素一组进行分组。用一个字符串数组strs存储每行的内容。
其中第0行和第 `n-1` 行没有中间内容，其余的有，则通过计算可知，第一行第一组包含元素 `s[1] s[2n-2-1]`，
即对应示例中的A和P，第一行第二组包含元素L和S，以此类推。除首位行外，每行每组都包含两个元素，因此可通过
简单地计算直到这两个元素与行数、偏移 `2n-2` 等间的关系。注意判断下标是否越界。

有两种方案，一种是将首尾两行独立进行求解，即第0行元素为 `s[0] s[n] s[2n]...`，最后一行元素为 `s[n-1] 
s[2n-1]...`，然后中间行则每次都尝试添加两个元素入保存它的字符串中。所有字符串相加即可。第二种方案就是
所有行都在一个for循环中处理，只是首行和尾行每次添加元素不尝试添加第二个。第一种方案效果貌似好一点，能
超过 `81%` 左右的CPP用户，第二种最多 `50%`。下面方案采用第二种，写起来更方便，看起来更易懂。

> Solution

```C++
class Solution {
public:
	string convert(string s, int numRows) {

        //部分特殊情况直接处理
		if (s.size() <=numRows ) return s;
		if (numRows == 1) return s;
		else if (numRows == 2) {
			int size = s.size();
			string s1, s2;
			for (int i = 0; i<size; ++i) {
				if (i % 2) s2.push_back(s[i]);
				else s1.push_back(s[i]);
			}
			return s1 + s2;
		}

        //每2n-2个元素分一组，设置偏移量
		int offset = 2 * numRows - 2;
		int size = s.size();

        //每个字符串保存对应行的内容
		string* strs = new string[numRows];

		int j = 0;
		for (int i = 0; i < numRows; ++i) {
			int begOffset = offset - i;
			j = 0;
			while (j + i < size) {
				strs[i].push_back(s[j + i]);

                //首尾行不尝试添加第二个元素
				if (i == 0 || i == numRows - 1) { j+=offset; continue; }
				if (begOffset + j < size) strs[i].push_back(s[begOffset + j]);
				j += offset;
			}
		}

        //将所有行元素汇总并返回
		s = "";
		for (int i = 0; i < numRows; ++i) s += strs[i];
		return s;
	}
};
```
