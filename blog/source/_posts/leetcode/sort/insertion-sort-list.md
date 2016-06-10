title: insertion-sort-list
date: 2016-01-01 16:12:54
tags: [leetcode,排序]
---
<h1>[147. Insertion Sort List](https://leetcode.com/problems/insertion-sort-list/)</h1> <!-- more -->
Total Accepted: 60691 Total Submissions: 216166 Difficulty: Medium
Sort a linked list using insertion sort.
# 模拟数组的插入排序,由于没有前向指针,所以只能从前往后遍历.寻找合适的插入位置
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
    ListNode* insertionSortList(ListNode* head) {
        if(head==NULL || head->next==NULL) {
            return head;
        }
        ListNode dummy(-1);
        dummy.next = head;
        ListNode *cur = head, *next = cur->next;
        while(cur && next){
            int val = next->val;
            ListNode *p = &dummy;
            while(p->next != next) {
                if(p->next->val >= val){
                    cur->next = next->next;
                    next->next = p->next;
                    p->next = next;
                    next = cur->next;
                    break;
                } else {
                    p = p->next;
                }
            }
            if(p->next == next) {
                cur = next;
                next = cur->next;
            }
        }
        return dummy.next;
    }
};
