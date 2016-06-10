title: flatten-binary-tree-to-linked-list
date: 2016-01-02 21:28:45
tags: [leetcode,树]
---
<h1>[114. Flatten Binary Tree to Linked List](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/)</h1><!-- more -->
Total Accepted: 69348 Total Submissions: 232085 Difficulty: Medium
Given a binary tree, flatten it to a linked list in-place.

For example,
Given
```C
         1
        / \
       2   5
      / \   \
     3   4   6
```
The flattened tree should look like:
```C
   1
    \
     2
      \
       3
        \
         4
          \
           5
            \
             6
```
# 迭代版本,用栈实现,其实就是先根遍历.
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
    void flatten(TreeNode* root) {
        stack<TreeNode *> s;
        if(root == nullptr) return;
        s.push(root);
        while(!s.empty()) {
            TreeNode *cur = s.top();
            s.pop();
            if(cur->right) {
                s.push(cur->right);
            }
            if(cur->left) {
                s.push(cur->left);
            }
            cur->left = nullptr;
            if(!s.empty()){
                cur->right = s.top();
            }
        }
    }
};
```
# 递归版本
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
    void flatten(TreeNode* root) {
        if(root == nullptr) return;
        flatten(root->left);
        flatten(root->right);
        if(root->left == nullptr) return;
        TreeNode *p = root->left;
        while(p->right) p = p->right;
        p->right = root->right;
        root->right = root->left;
        root->left = nullptr;
    }
};
```
