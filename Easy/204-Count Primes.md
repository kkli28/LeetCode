> Description

Description:

Count the number of prime numbers less than a non-negative number, n.

> Idea

方法1：从3到n，分别判断每个数是否是质数。性能十分差。

方法2：每找到一个质数，就从待找列表中去掉其倍数，如找到3，则去掉6、9、12等数，
然后取下一个数（5），详见网上的快速求质数算法。性能不错。

方法3：别人的，没看懂。。。

> Solution

```C++
//方法1：性能较差
class Solution {
public:
	bool isPrime(int num) {
		int end_index = num / 2;
		for (int i = 2; i <= end_index; ++i) {
			if ((num / i)*i == num) return false;
		}
		return true;
	}
	int countPrimes(int n) {
		if (n <= 2) return 0;
		int count = 1;
		for (int i = 3; i < n; i += 2)
			if (isPrime(i))
				++count;
		return count;
	}
};

//方法2：性能较好
class Solution {
public:
	int countPrimes(int n) {
		if (n <= 2) return 0;
		int* arr = new int[n + 1];
		int end = n + 1;
		for (int i = 0; i < end; ++i) arr[i] = 1;
		int count = 0;
		int index = 2;
		while (index < n) {
			++count;
			for (int i = index; i < n; i += index) arr[i] = 0;
			while (arr[index] == 0) ++index;
		}
		return count;
	}
};

//方法3：别人的代码，性能十分好
int countPrimes(int n) {
    if (n<=2) return 0;
	vector<bool> passed(n, false);
	int sum = 1;
	int upper = sqrt(n);
	for (int i=3; i<n; i+=2) {
		if (!passed[i]) {
			sum++;
			//avoid overflow
			if (i>upper) continue;
			for (int j=i*i; j<n; j+=i) {
				passed[j] = true;
			}
		}
	}
	return sum;
}
```
