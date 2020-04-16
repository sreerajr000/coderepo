---
layout: post
author: Sreeraj
title: Binary Indexed (Fenwick) Tree
---

For Range Sum Queries (RMQ)

```cpp
class FenwickTree {
	private: 
	vector<int> ft; 
	
	public: 
	FenwickTree(int n) { 
		ft.assign(n + 1, 0); 
	} // init n + 1 zeroes
	
	int rsq(int b) { // returns RSQ(1, b)
		int sum = 0; 
		for (; b; b -= LSOne(b)) 
			sum += ft[b];
		return sum; 
	} // note: LSOne(S) (S & (-S))
	
	int rsq(int a, int b) { // returns RSQ(a, b)
		return rsq(b) - (a == 1 ? 0 : rsq(a - 1)); 
	}
	
	// adjusts value of the k-th element by v (v can be +ve/inc or -ve/dec)
	void adjust(int k, int v) { // note: n = ft.size() - 1
		for (; k < (int)ft.size(); k += LSOne(k))
			ft[k] += v; 
	}
};

int main() {
	int f[] = { 2,4,5,5,6,6,6,7,7,8,9 }; // m = 11 scores
	FenwickTree ft(10); // declare a Fenwick Tree for range [1..10]
	// insert these scores manually one by one into an empty Fenwick Tree
	for (int i = 0; i < 11; i++) 
		ft.adjust(f[i], 1); // this is O(k log n)
	printf("%d\n", ft.rsq(1, 1)); // 0 => ft[1] = 0
	printf("%d\n", ft.rsq(1, 2)); // 1 => ft[2] = 1
	printf("%d\n", ft.rsq(1, 6)); // 7 => ft[6] + ft[4] = 5 + 2 = 7
	printf("%d\n", ft.rsq(1, 10)); // 11 => ft[10] + ft[8] = 1 + 10 = 11
	printf("%d\n", ft.rsq(3, 6)); // 6 => rsq(1, 6) - rsq(1, 2) = 7 - 1
	ft.adjust(5, 2); // update demo
	printf("%d\n", ft.rsq(1, 10)); // now 13
	return 0;
} 
```