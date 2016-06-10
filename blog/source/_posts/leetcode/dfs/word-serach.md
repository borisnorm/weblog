title: word-serach
date: 2016-01-01 21:50:49
tags: [leetcode,深度优先搜索]
---
<h1>[79. Word Search](https://leetcode.com/problems/word-search/)</h1><!-- more -->
Total Accepted: 60237 Total Submissions: 277421 Difficulty: Medium
Given a 2D board and a word, find if the word exists in the grid.

The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

For example,
Given board =
```C
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]
```
word = "ABCCED", -> returns true,
word = "SEE", -> returns true,
word = "ABCB", -> returns false.
# 对每个坐标从上下左右四个方向进行搜索, 用visited数组保存一个节点在本次搜索过程中是否已经访问过,若访问过,则直接返回false.
```C
class Solution {
public:
    bool exist(vector<vector<char>>& board, string word) {
        const int n = board.size();
        const int m = board[0].size();
        vector<vector<bool>> visited(n, vector<bool>(m, false));
        for(int i = 0; i < n; ++i) {
            for(int j = 0; j < m; ++j) {
                if(dfs(board, word, 0, i, j, visited)) {
                    return true;
                }
            }
        }
        return false;
    }
    bool dfs(vector<vector<char>>& board, string word, int index, int x, int y, vector<vector<bool>>& visited) {
        if(index == word.size()) {
            return true;
        }
        if(x < 0 || y < 0 || x >= board.size() || y >= board[0].size()) return false;
        if(visited[x][y]) return false;
        if(word[index] != board[x][y]) return false;
        visited[x][y] = true;
        bool ret =  dfs(board, word, index+1, x+1, y, visited) ||
                    dfs(board, word, index+1, x-1, y, visited) ||
                    dfs(board, word, index+1, x, y+1, visited) ||
                    dfs(board, word, index+1, x, y-1, visited);
        visited[x][y] = false;
        return ret;
    }
};
