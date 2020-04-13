---
layout: post
author: Sreeraj
title: Maximum Binary Tree II 
---

[Problem Link](https://leetcode.com/problems/maximum-binary-tree-ii/)

```cpp
TreeNode* insertIntoMaxTree(TreeNode* root, int val) {
    if(root == nullptr) return new TreeNode(val);
    if(root->val < val) {
        TreeNode *temp = new TreeNode(val);
        temp->left = root;
        return temp;
    }
    root->right = insertIntoMaxTree(root->right, val);
    return root;
}
```