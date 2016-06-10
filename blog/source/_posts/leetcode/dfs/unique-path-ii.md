title: unique-path-ii
date: 2016-01-02 10:12:06
tags: [leetcode,动态规划]
---
<h1>[63. Unique Paths II](https://leetcode.com/problems/unique-paths-ii/)</h1><!-- more -->
Total Accepted: 54446 Total Submissions: 189858 Difficulty: Medium
Follow up for "Unique Paths":

Now consider if some obstacles are added to the grids. How many unique paths would there be?

An obstacle and empty space is marked as 1 and 0 respectively in the grid.

For example,
There is one obstacle in the middle of a 3x3 grid as illustrated below.
```
[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
```
The total number of unique paths is 2.

Note: m and n will be at most 100.
# 从左上角开始，往右下角迭代。
```perl
class Solution {
public:
    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        const int m = obstacleGrid.size();
        const int n = obstacleGrid[0].size();
        vector<vector<int>> dp(m+1, vector<int>(n+1, 0));
        for(int i = 0; i < m; ++i) {
            for(int j = 0; j < n; ++j) {
                if(obstacleGrid[i][j]) dp[i+1][j+1] = 0;
                else if (i==0 && j==0) {
                    dp[i+1][j+1] = 1;
                } else {
                dp[i+1][j+1] = dp[i+1][j] + dp[i][j+1];
                }
            }
        }
        return dp[m][n];
    }
};
```
