title: merge-sorted-array
date: 2016-01-01 15:42:58
tags: [leetcode,排序]
---
<h1> [88. Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/)</h1>
Question
Total Accepted: 81135 Total Submissions: 275077 Difficulty: Easy<!-- more -->
Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.
Note:
You may assume that nums1 has enough space (size that is greater or equal to m + n) to hold additional elements from nums2. The number of elements initialized in nums1 and nums2 are m and n respectively.

# 先把数据放到临时数组中,再swap一下
```C
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        vector<int> ret(m+n, 0);
        int index = m+n-1, i = m-1, j = n-1;
        while(i >= 0 && j >= 0) {
            if(nums1[i] > nums2[j]) {
                ret[index--] = nums1[i];
                --i;
            } else {
                ret[index--] = nums2[j];
                --j;
            }
        }
        if(index >= 0) {
            if(i < 0) {
                while(j >= 0){
                    ret[index--] = nums2[j--];
                }
            } else if(j < 0) {
                while(i >= 0){
                    ret[index--] = nums1[i--];
                }
            }
        }
        nums1.swap(ret);
    }
};
```
