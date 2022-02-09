# Description:

Given a 2D board and a string word, find if the string word exists in the grid.

The string word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring.

The same letter cell may not be used more than once.
# sample:
board = ["ABCE","SFCS","ADEE"]
word = "ABCCED"

# 方法 dfs
贡献一个非常规整的dfs模板解法。和word searchII一样。 时间复杂度应该是： m * n * 4 ^ word.length;
```
class Solution:
    def exist(self, board, word):
        # dfs寻找
        m, n = len(board), len(board[0])
        
        # 当前位置为(i, j)，匹配到第k个字符
        def dfs(i, j, k):
            # 当数组越界或不相等时则不匹配
            if not 0 <= i < m or not 0 <= j < n or not board[i][j] == word[k]:
                return False
            # 匹配成功
            if k == len(word) - 1:
                return True
            # 避免走回头路
            board[i][j] = ''
            # 上下左右四个方向进行搜索
            res = dfs(i - 1, j, k + 1) or dfs(i + 1, j, k + 1) or dfs(i, j - 1, k + 1) or dfs(i, j + 1, k + 1)
            # 恢复当前的网格内字符
            board[i][j] = word[k]
            return res
        
        # 看是否匹配
        for i in range(m):
            for j in range(n):
                if dfs(i, j, 0):
                    return True
        return False

```
