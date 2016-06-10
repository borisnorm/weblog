title: first-missing-postive
date: 2016-01-01 17:15:00
tags: [leetcode,排序]
---
<h1>[41. First Missing Positive](https://leetcode.com/problems/first-missing-positive/)</h1>
<!-- more -->
Total Accepted: 55000 Total Submissions: 236467 Difficulty: Hard
Given an unsorted integer array, find the first missing positive integer.

For example,
Given [1,2,0] return 3,
and [3,4,-1,1] return 2.

Your algorithm should run in O(n) time and uses constant space.
# 桶排序
```C
class Solution {
public:
    int firstMissingPositive(vector<int>& nums) {
        const int maxn = 1000000;
        bool A[maxn];
        memset(A, 0, sizeof A);
        for_each(nums.begin(), nums.end(), [&A](int x){ if(x > 0)A[x] = 1;});
        for(int i = 1; i < maxn; ++i){
            if(A[i] == 0) {
                return i;
            }
        }
    }
};
```
