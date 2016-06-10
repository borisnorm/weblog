title: unique-path
date: 2016-01-01 19:36:16
tags: [leetcode,深度优先搜索,动态规划]
---
<h1>[62. Unique Paths](https://leetcode.com/problems/unique-paths/)</h1><!-- more -->
Total Accepted: 71840 Total Submissions: 206948 Difficulty: Medium
A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?
# 很简单
```C
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<vector<int>> ans(m, vector<int>(n));
        for(int i = 0; i < m; ++i) {
            ans[i][0] = 1;
        }
        for(int i = 0; i < n; ++i) {
            ans[0][i] = 1;
        }
        for(int i = 1; i < m; ++i) {
            for(int j = 1; j < n; ++j) {
                ans[i][j] = ans[i-1][j] + ans[i][j-1];
            }
        }
        return ans[m-1][n-1];
    }
};
```
