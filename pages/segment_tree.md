---
layout: post
author: Sreeraj
title: Segment Tree (Dynamic Range Minimum Query)
---


```cpp
class SegmentTree { // the segment tree is stored like a heap array
	private: 
	vector<int> st, A; // recall that vi is: typedef vector<int> vi;
	int n;
	
	int left (int p) { 
		return p << 1; 
	} // same as binary heap operations
	
	int right(int p) { 
		return (p << 1) + 1; 
	}
	
	void build(int p, int L, int R) { // O(n)
		if (L == R) // as L == R, either one is fine
			st[p] = L; // store the index
		else { // recursively compute the values
			build(left(p) , L , (L + R) / 2);
			build(right(p), (L + R) / 2 + 1, R );
			int p1 = st[left(p)], p2 = st[right(p)];
			st[p] = (A[p1] <= A[p2]) ? p1 : p2;
		} 
	}
	int rmq(int p, int L, int R, int i, int j) { // O(log n)
		if (i > R || j < L) 
			return -1; // current segment outside query range
		if (L >= i && R <= j) 
			return st[p]; // inside query range
		// compute the min position in the left and right part of the interval
		int p1 = rmq(left(p) , L , (L+R) / 2, i, j);
		int p2 = rmq(right(p), (L+R) / 2 + 1, R , i, j);
		if (p1 == -1) 
			return p2; // if we try to access segment outside query
		if (p2 == -1) 
			return p1; // same as above
		return (A[p1] <= A[p2]) ? p1 : p2; // as in build routine
	}

	public:
	SegmentTree(const vi &_A) {
		A = _A; n = (int)A.size(); // copy content for local usage
		st.assign(4 * n, 0); // create large enough vector of zeroes
		build(1, 0, n - 1); // recursive build
	}

	int rmq(int i, int j) { 
		return rmq(1, 0, n - 1, i, j); 
	} // overloading
};

int main() {
	int arr[] = { 18, 17, 13, 19, 15, 11, 20 }; // the original array
	vector<int> A(arr, arr + 7);
	SegmentTree st(A);
	printf("RMQ(1, 3) = %d\n", st.rmq(1, 3)); // answer = index 2
	printf("RMQ(4, 6) = %d\n", st.rmq(4, 6)); // answer = index 5
	return 0;
} 
```