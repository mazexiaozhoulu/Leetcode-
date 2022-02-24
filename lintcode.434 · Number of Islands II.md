## 1、题目描述
假设你设计一个游戏，用一个 m 行 n 列的 2D 网格来存储你的游戏地图。

起始的时候，每个格子的地形都被默认标记为「水」。我们可以通过使用 addLand 进行操作，将位置 (row, col) 的「水」变成「陆地」。

你将会被给定一个列表，来记录所有需要被操作的位置，然后你需要返回计算出来 每次 addLand 操作后岛屿的数量。

注意：一个岛的定义是被「水」包围的「陆地」，通过水平方向或者垂直方向上相邻的陆地连接而成。你可以假设地图网格的四边均被无边无际的「水」所包围。

请仔细阅读下方示例与解析，更加深入了解岛屿的判定。

## 时间复杂度 o（n * m）
```
DIRECTIONS = [
    [0, 1], [0, -1], [1, 0], [-1, 0]
    ]
"""
Definition for a point.
class Point:
    def __init__(self, a=0, b=0):
        self.x = a
        self.y = b
"""

class UnionFind:
    
    def __init__(self):
        
        self.father = {}
        self.count = 0 
        
    def union(self, a, b):
        
        root_a = self.find(a)
        root_b = self.find(b)
        
        if root_a == root_b:
            
            return 
        
        self.father[root_b] = root_a
        self.count -= 1 
        
    def find(self, point):
        
        path = [] 
        
        while point != self.father[point]:
            
            path.append(point)
            
            point = self.father[point]
            
        for p in path:
            
            self.father[p] = point 
            
        return point 
        
        
        
class Solution:
    """
    @param n: An integer
    @param m: An integer
    @param operators: an array of point
    @return: an integer array
    """
    def numIslands2(self, n, m, operators):
        # write your code here
        islands = set()
        results = []
        uf = UnionFind()
        
        for operator in operators:
            
            x, y = operator.x, operator.y
            
            if (x, y) in islands:
                
                results.append(uf.count)
                
                continue 
            
            islands.add((x, y))
            
            uf.father[(x, y)] = (x, y)
            uf.count += 1 
            
            for dx, dy in DIRECTIONS:
                
                nx, ny = x + dx, y + dy 
                
                if (nx, ny) in islands:
                    
                    uf.union((x, y), (nx, ny))
                    
            results.append(uf.count)
            
        return results
```
