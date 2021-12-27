```
class Solution:
    """
    @param: board: board a 2D board containing 'X' and 'O'
    @return: nothing
    """
    def surroundedRegions(self, board):
        if len(board) == 0 or len(board[0]) == 0:
            return ;
        n,m = len(board),len(board[0])
        def dfs(x,y):
            #保证当前点在图中
            if x < 0 or y < 0 or x >= n or y >= m:
                return ;
            if board[x][y] != 'O':
                return ;
            board[x][y] = '*'
            dfs( x + 1, y);
            dfs( x - 1, y);
            dfs( x , y + 1);
            dfs( x , y - 1);
        def is_border(x,y):#判断是否边界
            if x == 0 or y == 0 or x == n - 1 or y == m - 1:
                return True
            return False

        #四周向中间搜
        for i in range(n):
            for j in range(m):
                if is_border(i,j) == False:
                    continue
                if board[i][j] == 'O':
                    dfs(i,j)
        #遍历图，更新结果
        for i in range(n):
            for j in range(m):
                if board[i][j] == 'O':
                    board[i][j] = 'X'
                elif board[i][j] == '*':
                    board[i][j] = 'O'
```
