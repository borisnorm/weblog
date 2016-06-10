title: bianry-tree-preorder-traversal
date: 2016-01-03 15:32:29
tags: [leetcode,树]
---

<h1>[144. Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/)</h1>
<!-- more -->
Total Accepted: 100488 Total Submissions: 263328 Difficulty: Medium
Given a binary tree, return the preorder traversal of its nodes' values.

For example:
Given binary tree {1,#,2,3},
   1
    \
     2
    /
   3
return [1,2,3].

Note: Recursive solution is trivial, could you do it iteratively?
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
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> ans;
        dfs(root, ans);
        return ans;
    }
    void dfs(TreeNode *root, vector<int> &ans) {
        if(root == nullptr) {
            return;
        }
        ans.push_back(root->val);
        dfs(root->left, ans);
        dfs(root->right, ans);
    }
};

