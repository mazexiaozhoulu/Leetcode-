```
from collections import deque
class Solution:
    """
    @param maze: the maze
    @param start: the start
    @param destination: the destination
    @return: whether the ball could stop at the destination
    """
    def hasPath(self, maze, start, destination):

        Q = deque([start])
        n = len(maze)
        m = len(maze[0])
        dirs = ((0, 1), (0, -1), (1, 0), (-1, 0))
        while Q:
            i, j = Q.popleft()
            #记录当前点被走过
            maze[i][j] = 2
            #如果当前的节点 就是终点，就返回True
            if i == destination[0] and j == destination[1]:
                return True
            #不然就遍历其他
            for x, y in dirs:
                row = i + x
                col = j + y
                #如果maze[row][col] != 1说明可以继续走
                while 0 <= row < n and 0 <= col < m and maze[row][col] != 1:
                    row += x
                    col += y
                #如果超出范围并且碰到墙，那就返回到上一个节点
                #如果上一个节点是没走过的点，就加入队列
                row -= x
                col -= y
                if maze[row][col] == 0:
                    Q.append([row, col])
        return False
```
