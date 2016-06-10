title: palindrome-partitioning
date: 2016-01-01 19:01:05
tags: [leetcode,深度优先搜索,动态规划]
---
<h1>[131. Palindrome Partitioning](https://leetcode.com/problems/palindrome-partitioning/)</h1><!-- more -->
Total Accepted: 55328 Total Submissions: 202066 Difficulty: Medium
Given a string s, partition s such that every substring of the partition is a palindrome.

Return all possible palindrome partitioning of s.

For example, given s = "aab",
Return
```C
  [
    ["aa","b"],
    ["a","a","b"]
  ]
```
# 有几个注意事项:
```C
class Solution {
public:
    vector<vector<string>> partition(string s) {
        int n = s.size();
        vector<vector<string>> ans;
        vector<string> tmp;
        vector<vector<bool>> A(n, vector<bool>(n));
        init(s, n, A);
        dfs(s, ans, tmp, 0, A);
        return ans;
    }
```
## 第一点: 二维向量的初始化方式.
```C
vector<vector<bool>> A(n, vector<bool>(n));
```
```C
    void dfs(string s, vector<vector<string>> &ans, vector<string> &tmp, int index, vector<vector<bool>> &A){
        if(index == s.size()) {
            ans.push_back(tmp);
            return;
        } else {
            for(int i = index; i < s.size(); ++i) {
                if(A[index][i]){
                    string sb = s.substr(index, i-index+1);
                    tmp.push_back(sb);
                    dfs(s, ans, tmp, i+1, A);
                    tmp.pop_back();
                }
            }
        }
    }
```
## 第二点: 写递归程序之前有两点心里一定要想的非常清楚后,才能下手.
> 首先,递归终止的条件是什么??
> 其次,你打算如何向着终止的方向搜索(递归)??

本题中,递归终点是,$index$变量与$size$大小相等时,说明有一组新的解产生. 我们又是如何逐步迈向结果的呢?? 通过$index$变量.$index$指的是从此处开始,到末尾的解,在加上我们提前找的回文,组成整个问题的解.
```C
    void init(const string &s, int n, vector<vector<bool>> &A) {
        for(int i = n-1; i >= 0; --i) {
            A[i][i] = 1;
            for(int j = i+1; j < n; ++j) {
                if(s[i] != s[j]) {
                    
                } else {
                    if(j - i < 2 || A[i+1][j-1] == 1) {
                        A[i][j] = 1;
                    }
                }
            }
        }
    }
};
```
## 第三点: 这里利用动态规划预处理字符串,i应从n-1迭代到0,观察公式:
$$f(i)(j) = 1 {s(i) == s(j)} and { j-i < 2 or f(i+1)(j-1) }$$

## 前者要用到后者的结果!
