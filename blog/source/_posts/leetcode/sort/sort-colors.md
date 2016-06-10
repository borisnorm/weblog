title: sort-colors
date: 2016-01-01 17:03:31
tags: [leetcode,排序]
---
<h1>[75. Sort Colors](https://leetcode.com/problems/sort-colors/)</h1><!-- more -->
Total Accepted: 80580 Total Submissions: 239465 Difficulty: Medium
Given an array with n objects colored red, white or blue, sort them so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

Note:
You are not suppose to use the library's sort function for this problem.
# 桶排序,记得要清空之前的元素
```C
class Solution {
public:
    void sortColors(vector<int>& nums) {
        const int maxn = 3;
        if(nums.size() < 2){
            return;
        } else {
            int A[maxn];
            memset(A, 0, sizeof A);
            for_each(nums.begin(), nums.end(), [&A](int x){A[x] += 1;});
            nums.clear();
            for(int i = 0; i < 3; ++i) {
                while(A[i]--) nums.push_back(i);
            }
        }
    }
};
```
