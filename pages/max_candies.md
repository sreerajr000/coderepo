---
layout: post
author: Sreeraj
title: Max Candies
---

[Problem Link](https://leetcode.com/problems/maximum-candies-you-can-get-from-boxes)

```cpp
class Solution {
public:
    int maxCandies(vector<int>& status, vector<int>& candies, vector<vector<int>>& keys, vector<vector<int>>& containedBoxes, vector<int>& initialBoxes) {
        queue<int> q;
        unordered_set<int> obtained;
        int sum = 0;
        for(auto x: initialBoxes)
            q.push(x);
        
        while(!q.empty()) {
            int box = q.front();
            q.pop();
            obtained.insert(box);
            for(auto x: keys[box]) {
                status[x] = 1;
            }
            for(auto x: containedBoxes[box])
                q.push(x);
        }
        for(auto x: obtained) {
            if(status[x])
                sum+=candies[x];
        }
        return sum;
    }
};
```