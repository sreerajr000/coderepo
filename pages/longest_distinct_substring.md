---
layout: post
author: Sreeraj
title: Longest Substring Without Repeating Characters
---

Given a string, find the length of the longest substring without repeating characters.

```cpp
int lengthOfLongestSubstring(string s) {
    bitset<256> map;
    int ans = 0;
    int i = 0, j = 0;
    while(i < s.length() && j < s.length()) {
        if(!map[s[j]]) {
            map[s[j++]] = true;
            ans = max(ans, j-i);
        } else
            map[s[i++]] = false;
    }
    return ans;
}
```
