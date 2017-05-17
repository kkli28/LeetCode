> Description

Given a digit string, return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below.

```
1:          2: abc          3: def
4: ghi      5: jkl          6: mno
7: pqrs     8: tuv          9: wxyz
0: 

Input:Digit string "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```

> Idea

循环递归法，1个数字对应n个字母，则该层循环n次，每次进行递归调用，该递归调用解决除去该数字之外
其余所有数字的排列组合。例如组合 `"23"`：

```
digits: 2 3
add: a

    digits: 3
    add: d
        result: ad
    add: e
        result: ae
    add: f
        result: af
add: b

    digits: 3
    add: d
        result: bd
    add: e
        result: be
    add: f
        result: bf
add: c

    digits: 3
    add: d
        result: cd
    add: e
        result: ce
    add: f
        result: cf

results: ad ae af bd be bf cd ce cf
```

> Solution

```C++
class Solution {
public:
	string strs[10] = {
		"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"
	};
	vector<string> result;

	void func(int* arr, int n,string& s) {
		if (n == 0) {
			result.push_back(s);
			return;
		}

		string str = strs[arr[0]];
		int size = str.size();
		if (size == 0) {
			func(arr + 1, n - 1, s);
			return;
		}
		for (int i = 0; i < size; ++i) {
			string tmp = s;
			tmp.push_back(str[i]);
			func(arr + 1, n - 1, tmp);
		}
	}
	vector<string> letterCombinations(string digits) {
		int size = digits.size();
		if (size == 0) return {};
		int* arr = new int[size];
		for (int i = 0; i < size; ++i) {
			arr[i] = digits[i] - 48;
		}
        
        string s;
		func(arr, size, s);
		return result;
	}
};
```
