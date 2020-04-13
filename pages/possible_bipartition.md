---
layout: post
author: Sreeraj
title: Bipartite Check
---

Check whether a graph is bipartite or not.

```cpp
class Solution {
public:
    vector<bool> visited;
    vector<bool> color;
    vector<vector<int>> adj;
    bool dfs(int v) {
        for (int u : adj[v]) {
            if (!visited[u]) {
                visited[v] = true;
                color[u] = !color[v];
                if(!dfs(u))
                    return false;
            }
            else if(color[u] == color[v])
                return false;
        }
        return true;
    }
    
    bool possibleBipartition(int N, vector<vector<int>>& dislikes) {
        visited.resize(N+1);
        adj.resize(N+1);
        color.resize(N+1);
        for(auto x: dislikes) {
            adj[x[0]].push_back(x[1]);
            adj[x[1]].push_back(x[0]);
        }
        for(int i = 1; i <= N; ++i) {
            if(!visited[i] && !dfs(i))
                return false;
        }
        return true;
    }
};
```