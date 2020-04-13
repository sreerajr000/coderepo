---
layout: post
author: Sreeraj
title: Longest ZigZag path in a Tree
---

```cpp
class Solution {
public:
    int maxLen = 0;
    
    void zigzag(TreeNode* root, bool dir, int l){
        if(root == nullptr) return ;
        maxLen = max(l, maxLen);
        zigzag(root->left, !dir, dir?0:l+1);
        zigzag(root->right, !dir, dir?l+1:0);
    }
    
    int longestZigZag(TreeNode* root) {
        if(root == nullptr) return 0;
        zigzag(root, true, 0);
        zigzag(root, false, 0);
        return maxLen;
    }
};
```