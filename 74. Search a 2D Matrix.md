二维坐标转一维坐标：
n行m列的矩阵： x*m+y


把整个matrix看作一个折叠起来的一维数
一维坐标 转 二维坐标:
x = index // len(matrix[0])

y = index % len(matrix[0])

return matrix[x][y]

```
class Solution(object):
    def searchMatrix(self, matrix, target):
        """
        :type matrix: List[List[int]]
        :type target: int
        :rtype: bool
        """
        if not matrix or not matrix[0]:
            return False
        
        
        m, n = len(matrix), len(matrix[0])
        start, end = 0, n*m-1
        while start + 1 < end:
            mid = (start + end)//2
            if self.indexmatrix(matrix, mid) < target:
                start = mid
            else:
                end = mid
                
        if self.indexmatrix(matrix, start) == target:
            return True
        if self.indexmatrix(matrix, end) == target:
            return True
        return False
        
        
    def indexmatrix(self, matrix, index):
        x = index // len(matrix[0])
        y = index % len(matrix[0])
        return matrix[x][y]
        
        
```
