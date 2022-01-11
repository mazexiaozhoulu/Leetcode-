sort函数进行排序的时间复杂度为n*log2n
build min heap 时间复杂度 logn

# 方法1 2D->1D + sort 
时间复杂度 sort的时间复杂度 * 找到(k-1的时间复杂度=n^2logn

```
class Solution:
    def kthSmallest(self, matrix: List[List[int]], k: int) -> int:
        rec = sorted(sum(matrix, []))
        return rec[k - 1]
```

# 方法2 heap 
时间复杂度 nlogn

```
import heapq
class Solution:
    def kthSmallest(self, matrix: List[List[int]], k: int) -> int:
        h = []
        for i in matrix:
            for j in i:
                heapq.heappush(h, j)
        while k:
            k -= 1
            x = heapq.heappop(h)
        return x 
```

# 归并k次的heap
时间复杂度是klogn, pop & push 都是logn的时间复杂度，重复k次
```
import heapq
class Solution:
    def kthSmallest(self, matrix, k):
        n = len(matrix)
        pq = [(matrix[i][0], i, 0) for i in range(n)]
        heapq.heapify(pq)
        
        for i in range(k-1):
            number, x, y = heapq.heappop(pq)
            if y != n:
                heapq.heappush(pq,(matrix[x][y + 1], x, y+1))
        return heapq.heappop(pq)[0]

```
