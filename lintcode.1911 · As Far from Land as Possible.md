>一开始，我们找出所有陆地格子，将它们放入队列，作为第 0 层的结点。

>建立distance，用来记录是否被访问过+距离

>不断访问队列deque，每次pop出一个点（不超出范围，没被访问过的），加入队列，放到distance记录

>最后返回distance里记录的最大值
```
class Solution:
    """
    @param grid: An array.
    @return: An integer.
    """
    def maxDistance(self, grid):
        DIRECTIONS = [[0, 1], [1, 0], [0, -1], [-1, 0]]
        q = collections.deque()
        visited = set()
        n, m = len(grid), len(grid[0])

        for i in range(n):
            for j in range(m):
                if grid[i][j] == 1:
                    q.append((i, j))
                    visited.add((i, j))

        step = -1
        while q:
            step += 1
            queue_size = len(q)
            for _ in range(queue_size):
                x, y = q.popleft()
                for direction in DIRECTIONS:
                    new_x = x + direction[0]
                    new_y = y + direction[1]
                    if not self.is_valid(new_x, new_y, grid):
                        continue
                    if (new_x, new_y) in visited:
                        continue
                    q.append((new_x, new_y))
                    visited.add((new_x, new_y))
        
        return -1 if step == 0 else step

    def is_valid(self, x, y, grid):
        if x < 0 or x >= len(grid):
            return False
        if y < 0 or y >= len(grid[0]):
            return False
            
        return grid[x][y] == 0
```
