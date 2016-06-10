title: merge-two-sorted-lists
date: 2016-01-01 15:53:43
tags: [leetcode,排序]
---
<h1>[21. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)</h1><!-- more -->
Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.
# 先设定dummy节点,随后用newHead指针不断后移
```C
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode dummy(-1);
        ListNode *newHead = &dummy;
        while(l1 && l2) {
            if(l1->val < l2->val) {
                newHead->next = l1; newHead = newHead->next;
                l1 = l1->next;
            } else {
                newHead->next = l2; newHead = newHead->next;
                l2 = l2->next;
            }
        }
        if(l1) {
            newHead->next = l1;
        } else if(l2) {
            newHead->next = l2;
        }
        return dummy.next;
    }
};
```
