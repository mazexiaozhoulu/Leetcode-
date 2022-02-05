## Description
Given a knight in a chessboard n * m (a binary matrix with 0 as empty and 1 as barrier). the knight initialze position is (0, 0) and he wants to reach position (n - 1, m - 1)

Knight can only be from left to right. Find the shortest path to the destination position, return the length of the route. Return -1 if knight can not reached.

## Example
Example 1:

Input:

[[0,0,0,0],[0,0,0,0],[0,0,0,0]]

Output:

3

Explanation:

[0,0]->[2,1]->[0,2]->[2,3]

## 方法 
BFS

## 时间复杂度：
O（N）N是matrix里点的个数。
空间复杂度：O（N）
```
DIRECTIONS = [(1, 2), (-1, 2), (2, 1), (-2, 1)]

class Solution:
    """
    @param grid: a chessboard included 0 and 1
    @return: the shortest path
    """
    def shortestPath2(self, grid):
        # write your code here
        if len(grid) == 0 or len(grid[0]) == 0:
            return -1
        n = len(grid)
        m = len(grid[0])

        queue = collections.deque([(0,0)])
        distance = {(0,0):0}

        while queue:
            x,y = queue.popleft()
            for i, j in DIRECTIONS:
                delta_x = x+i
                delta_y = y+j
                if not self.vaild(delta_x, delta_y, grid, distance):
                    continue
                queue.append((delta_x,delta_y))
                distance[(delta_x,delta_y)] = distance[(x,y)] + 1
            
        if (n-1,m-1) in distance:
            return distance[(n-1,m-1)]
        return -1
    def vaild(self, x, y, grid, distance):
        if x < 0 or y < 0 or x >= len(grid) or y >= len(grid[0]):
            return False
        if grid[x][y] == 1:
            return False
        if(x,y) in distance:
            return False
        return True
                     
```
