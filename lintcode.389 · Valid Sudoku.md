## Description
Determine whether a Sudoku is valid.

The Sudoku board could be partially filled, where empty cells are filled with the character ..

## Input:
["53..75...","6..195...",".98....6.","8...6...3","4..8.3..1","7...2...6",".6....28.","...419..5","....8..79"]

Output: false
Explanation: 
The sudoku is look like this. It's invaild because there are two '5' in the first row and the sixth line.


```

class Solution:
    """
    @param board: the board
    @return: whether the Sudoku is valid
    """
    def isValidSudoku(self, board):
        used = set()
        
        # 先枚举行，检查每行是否合法
        for row in range(9):
            used = set()
            for col in range(9):
                if not self.check_valid(board[row][col], used):
                    return False
        
        # 先枚举列，检查每列是否合法
        for col in range(9):
            used = set()
            for row in range(9):
                if not self.check_valid(board[row][col], used):
                    return False
        
        # 每个分块的左上角的坐标为(i * 3, j * 3)
        for i in range(3):
            for j in range(3):
                used = set()
                for row in range(i * 3, i * 3 + 3):
                    for col in range(j * 3, j * 3 + 3):
                        if not self.check_valid(board[row][col], used):
                            return False
        
        return True
    
    # 检查字符是否有冲突
    def check_valid(self, c, used):
        if c == '.':
            return True
        if c in used:
            return False
        used.add(c)
        return True
```
