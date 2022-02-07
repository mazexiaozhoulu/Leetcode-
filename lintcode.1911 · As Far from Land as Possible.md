>一开始，我们找出所有陆地格子，将它们放入队列，作为第 0 层的结点。

>建立distance，用来记录是否被访问过+距离

>不断访问队列deque，每次pop出一个点（不超出范围，没被访问过的），加入队列，放到distance记录

>最后返回distance里记录的最大值
```
DIRECTIONS = [
  [1, 0], 
  [-1, 0], 
  [0, 1], 
  [0, -1]
]

class Solution:
    """
    @param grid: An array.
    @return: An integer.
    """
    def maxDistance(self, grid):
    #1:一开始，我们找出所有陆地格子，将它们放入队列，作为第 0 层的结点。
        n, m = len(grid), len(grid[0])
        land = [
          (i, j) 
          for i in range(n)
          for j in range(m)
          if grid[i][j] == 1
        ]
        queue = collections.deque(land) 
        #只把陆地放到了distance里
        distance = {
          (i, j): 0 
          for i, j in land
        }

        while queue: 
          x, y = queue.popleft()
          #遍历所有和陆地（x,y）相邻节点
          for dx, dy in DIRECTIONS: 
            x_, y_ = x + dx, y + dy 
            #判断是否在范围内
            if x_ < 0 or x_ >= n or y_ < 0 or y_ >= m: 
              continue 
            #判断是否被访问过(只有陆地和被访问过的海洋才在distance里)
            if (x_, y_) in distance: 
              continue 
            distance[(x_, y_)] = distance[(x, y)] + 1 
            queue.append((x_, y_)) 
        
        sea_distance = [
          distance[(i, j)] 
          for i, j in distance
          if grid[i][j] == 0 
        ]

        if not sea_distance: 
          return -1 
        return max(sea_distance)
```
