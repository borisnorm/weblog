title: sudoku-solver
date: 2016-01-01 22:21:13
tags: [leetcode,深度优先搜索]
---
<h1>[37. Sudoku Solver](https://leetcode.com/problems/sudoku-solver/)</h1><!-- more -->
Total Accepted: 42831 Total Submissions: 181622 Difficulty: Hard
Write a program to solve a Sudoku puzzle by filling the empty cells.

Empty cells are indicated by the character '.'.

You may assume that there will be only one unique solution.
# 解决数独问题
```C
class Solution {
public:
    bool solveSudoku(vector<vector<char>>& board) {
        const int m = board.size();
        const int n = board[0].size();
        for(int i = 0; i < m; ++i) {
            for(int j = 0; j < n; ++j) {
                if(board[i][j] == '.') {
                    for(int k = 0; k < 9; ++k) {
                        board[i][j] = '1' + k;
                        if(isvalid(board, i, j) && solveSudoku(board)){
                            return true;
                        }
                        board[i][j] = '.';
                    }
                    return false;
                }
            }
        }
        return true;
    }
    bool isvalid(vector<vector<char>>& board, int x, int y) {
        for(int i = 0; i < 9; ++i) {
            if(i != x && board[i][y] == board[x][y]) return false;
        }
        for(int j = 0; j < 9; ++j) {
            if(j != y && board[x][j] == board[x][y]) return false;
        }
        for(int i = 3*(x/3); i < 3*(x/3+1); ++i) {
            for(int j = 3*(y/3); j < 3*(y/3+1); ++j) {
                if((i != x || j != y) && board[i][j] == board[x][y]) {
                    return false;
                }
            }
        }
        return true;
    }
};
```
