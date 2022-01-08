时间复杂度：O(C)O(C)，由于此题给定的棋盘大小为常数 C = 9C=9，因此时间复杂度为常数。

空间复杂度：O(1)O(1)。

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

    def validTicTacToe(self, board):
    #先计算 'O' 和 'X'的数量
        oCount = sum(row.count('O') for row in board)
        xCount = sum(row.count('X') for row in board)
        # 如果'X'>='O' 则合法；
        return not (oCount != xCount and oCount != xCount - 1 or
        #如果‘O’（玩家2）胜利，则‘X’和‘O’的数量相同，再加上 not 就是反义
                    oCount != xCount and self.win(board, 'O') or
                    oCount != xCount - 1 and self.win(board, 'X'))

```
