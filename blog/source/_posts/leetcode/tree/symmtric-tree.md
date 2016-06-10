title: symmtric-tree
date: 2016-01-02 22:18:40
tags: [leetcode,树]
---
<h1>[101. Symmetric Tree](https://leetcode.com/problems/symmetric-tree/)</h1><!-- more -->
Total Accepted: 86835 Total Submissions: 265081 Difficulty: Easy
Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

For example, this binary tree is symmetric:
```C
    1
   / \
  2   2
 / \ / \
3  4 4  3
```
But the following is not:
```C
    1
   / \
  2   2
   \   \
   3    3
```
Note:
Bonus points if you could solve it both recursively and iteratively.
# 判断一棵树是否是相似树
```C
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        if(root == nullptr) return true;
        return isSymmetric(root->left, root->right);
    }
    bool isSymmetric(TreeNode *left, TreeNode *right) {
        if(left == nullptr && right == nullptr) return true;
        if(left == nullptr || right == nullptr) return false;
        return  left->val == right->val 
                && isSymmetric(left->left, right->right) 
                && isSymmetric(left->right, right->left);
    }
};
```
