title: populating-next-right-pointers-ii
date: 2016-01-02 21:09:44
tags: [leetcode,树]
---
<h1>[117. Populating Next Right Pointers in Each Node II](https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/)</h1><!-- more -->
Total Accepted: 52318 Total Submissions: 161397 Difficulty: Hard
Follow up for problem "Populating Next Right Pointers in Each Node".

What if the given tree could be any binary tree? Would your previous solution still work?

Note:

You may only use constant extra space.
# 迭代版本,用next指针记录每层的起始位置,用prev指针进行具体某一层的遍历,算法正确执行的基础是:我们依据上层的信息迭代下层信息,并且我们能够保证在迭代下一层之前上一层已经完成.
```C
/**
 * Definition for binary tree with next pointer.
 * struct TreeLinkNode {
 *  int val;
 *  TreeLinkNode *left, *right, *next;
 *  TreeLinkNode(int x) : val(x), left(NULL), right(NULL), next(NULL) {}
 * };
 */
class Solution {
public:
    void connect(TreeLinkNode *root) {
        while(root) {
            TreeLinkNode *next = nullptr;
            TreeLinkNode *prev = nullptr;
            while(root) {
                if(!next) {
                    next = root->left ? root->left : root->right;
                }
                if(root->left) {
                    if(prev)prev->next = root->left;
                    prev = root->left;
                }
                if(root->right) {
                    if(prev)prev->next = root->right;
                    prev = root->right;
                }
                root = root->next;
            }
            root = next;
        }
    }
};
```
# 递归版本,用dummy节点表示下层的起始位置,用p指针执行具体遍历.
```C
/**
 * Definition for binary tree with next pointer.
 * struct TreeLinkNode {
 *  int val;
 *  TreeLinkNode *left, *right, *next;
 *  TreeLinkNode(int x) : val(x), left(NULL), right(NULL), next(NULL) {}
 * };
 */
class Solution {
public:
    void connect(TreeLinkNode *root) {
        if(root == nullptr) return;
        TreeLinkNode dummy(-1);
        TreeLinkNode *p = &dummy;
        while(root) {
            if(root->left) {
                p->next = root->left;
                p = root->left;
            }
            if(root->right) {
                p->next = root->right;
                p = root->right;
            }
            root = root->next;
        }
        connect(dummy.next);
    }
};
```
