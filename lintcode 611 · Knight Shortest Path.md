```
"""
Definition for a point.
class Point:
    def __init__(self, a=0, b=0):
        self.x = a
        self.y = b
"""
offset = [
    (-2,-1),(-2,1),(-1,2),(-1,-2),
    (2,1),(2,-1),(1,2),(1,-2)
]
class Solution:
    """
    @param grid: a chessboard included 0 (false) and 1 (true)
    @param source: a point
    @param destination: a point
    @return: the shortest path 
    """
    def shortestPath(self, grid, source, destination):
        # write your code here
        queue = collections.deque([(source.x, source.y)])
        disToSrcMap = {(source.x, source.y):0}

        while queue:
            x,y = queue.popleft()
            if(x,y) == (destination.x, destination.y):
                return disToSrcMap[(x,y)]
            for dx, dy in offset:
                next_x, next_y = x + dx, y + dy
                if not self.is_valid(next_x, next_y, grid):
                    continue
                if (next_x, next_y) in disToSrcMap:
                    continue
                queue.append((next_x, next_y))
                disToSrcMap[(next_x, next_y)] = disToSrcMap[(x,y)]+1
        return -1

    def is_valid(self, x, y ,grid):
        n, m = len(grid), len(grid[0])
        if x< 0 or x>=n or y<0 or y>=m:
            return False
        return not grid[x][y]


```
