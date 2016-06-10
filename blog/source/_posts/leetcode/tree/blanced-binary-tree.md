title: blanced-binary-tree
date: 2016-01-02 21:56:32
tags: [leetcode,树]
---
<h1>[110. Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/)</h1><!-- more -->
Total Accepted: 88766 Total Submissions: 269643 Difficulty: Easy
Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.
# 平衡二叉树的定义,每个节点的左右子树高度相差不过1
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
    bool isBalanced(TreeNode* root) {
        return isBalancedImp(root) >= 0;
    }
    int isBalancedImp(TreeNode *root) {
        if(root == nullptr) return 0;
        int lft = isBalancedImp(root->left);
        int rht = isBalancedImp(root->right);
        if(lft == -1 || rht == -1 || abs(lft-rht) > 1) return -1;
        return max(lft, rht) + 1;
    }
};
```
# 两个不同写法
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
    bool isBalanced(TreeNode* root) {
        int h;
        return isBalancedImp(root, &h);
    }
    bool isBalancedImp(TreeNode *root, int *h) {
        if(root == nullptr) {
            *h = 0;
            return true;
        }
        int lft, rht;
        bool l = isBalancedImp(root->left, &lft);
        bool r = isBalancedImp(root->right, &rht);
        *h = max(lft, rht) + 1;
        return l && r && (abs(lft-rht) < 2);
    }
};
```
