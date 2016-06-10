title: sort-list
date: 2016-01-01 16:38:40
tags: [leetcode,排序]
---
<h1>[148. Sort List](https://leetcode.com/problems/sort-list/)</h1><!-- more -->
Total Accepted: 60737 Total Submissions: 257048 Difficulty: Medium
Sort a linked list in O(n log n) time using constant space complexity.
Subscribe to see which companies asked this question
# 单链表归并排序,先用快慢指针找到,单链表的中点,并将链表断开,在分别对子数组处理
```C++
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
    ListNode* sortList(ListNode* head) {
        if(head==NULL || head->next==NULL){
            return head;
        }
        ListNode *slow = head, *fast = head->next;
        while(fast && fast->next){
            slow = slow->next, fast = fast->next->next;
        }
        ListNode *tmp = slow->next;
        slow->next = NULL;
        ListNode *l1 = sortList(head); 
        ListNode *l2 = sortList(tmp);
        ListNode *ret = mergeTwoList(l1, l2);
        return ret;
    }
    ListNode *mergeTwoList(ListNode *l1, ListNode *l2) {
        ListNode dummy(-1);
        ListNode *p = &dummy;
        for(p; l1 != NULL || l2 != NULL; p = p->next) {
            int v1 = l1 == NULL ? INT_MAX : l1->val;
            int v2 = l2 == NULL ? INT_MAX : l2->val;
            if(v1 < v2) {
                p->next = l1;
                l1 = l1->next;
            } else {
                p->next = l2;
                l2 = l2->next;
            }
        }
        return dummy.next;
    }
};
```
这里mergeTwoList的写法非常经典,逻辑上将较短list用INT_MAX补齐到和长list相同的长度,可以避免很多分情况讨论
