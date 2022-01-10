```
class NumMatrix:
    """
    @param: matrix: a 2D matrix
    """
    def __init__(self, matrix):
        m, n = len(matrix), (len(matrix[0]) if matrix else 0)
        self.sum = [[0] * (n+1) for _ in range(m)]
        _sum = self.sum

        for i in range(m):
            for j in range(n):
                _sum[i][j+1] = _sum[i][j] + matrix[i][j]

    
    def sumRegion(self, row1, col1, row2, col2):
        # write your code here
        _sum = self.sum
        total = sum(_sum[i][col2+1] - _sum[i][col1] for i in range(row1, row2+1))
        return total
```
