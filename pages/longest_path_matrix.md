---
layout: post
author: Sreeraj
title: Longest Increasing Path in a Matrix
---


```cpp
class Solution {
public:
    vector<vector<int>> dirs = {{0,1}, {1,0}, {-1,0}, {0,-1}};
    vector<vector<int>> dp;
    
    int dfs(vector<vector<int>>& matrix, int i, int j) {
        int mx = 1;
        if(dp[i][j] != 0)
            return dp[i][j];
        int m = matrix.size(), n = matrix[0].size();
        for(auto dir:dirs) {
            int x = i + dir[0], y = j + dir[1];
            if(x < 0||y < 0||x >= m||y >= n||matrix[x][y]<=matrix[i][j])
                continue;

            int l = 1 + dfs(matrix, x, y);
            mx = max(l, mx);
        }
        dp[i][j] = mx;
        return mx;
    }
    
    int longestIncreasingPath(vector<vector<int>>& matrix) {
        if(matrix.size()==0)
            return 0;
        dp.resize(matrix.size(), vector<int>(matrix[0].size()));
        int m = 1;
        for(int i = 0; i < matrix.size(); ++i) {
            for(int j = 0; j < matrix[0].size(); ++j) {
                int l = dfs(matrix, i, j);
                m = max(l, m);
            }
        }
        return m;
    }
};
```