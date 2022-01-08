时间复杂度：O(C)，由于此题给定的棋盘大小为常数 C = 9，因此时间复杂度为常数。

空间复杂度：O(1)

```
# any() 函数用于判断给定的可迭代参数iterable 是否全部为False，则返回False，如果有一个为True，则返回True。 元素除了是0、空、FALSE 外都算TRUE。

class Solution:
    def win(self, board, p):
    #any函数里的2个情况，满足任何一个 就赢了
        return any(board[i][0] == p and board[i][1] == p and board[i][2] == p or  # 某一列都为p
                   board[0][i] == p and board[1][i] == p and board[2][i] == p for i in range(3)) or \  # 某一行都为p， 3以内遍历
                   # 两个对角线 都是 p
                   board[0][0] == p and board[1][1] == p and board[2][2] == p or \
                   board[0][2] == p and board[1][1] == p and board[2][0] == p
    # 通过检验 没有不合法的行为，去确定合法。
    def validTicTacToe(self, board):
    #先计算 'O' 和 'X'的数量，并且确认没有不合法的情况
        oCount = sum(row.count('O') for row in board)
        xCount = sum(row.count('X') for row in board)
        return not (oCount != xCount and oCount != xCount - 1 or # 只有‘O’和'X'的数量相等，或者'O'比'X'的数量少一个 才是合法的，
                    oCount != xCount and self.win(board, 'O') or# 在玩家2（'O'）赢得情况下，但‘O’和'X'的数量大小不一样，则不合法
                    oCount != xCount - 1 and self.win(board, 'X')# 在玩家2（'X'）赢得情况下，但‘O’并不比'X少一个，则不合法)

```
