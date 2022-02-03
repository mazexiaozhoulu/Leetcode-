## Description
Given a n x n matrix where each of the rows and columns are sorted in ascending order, find the kth smallest element in the matrix.

Note that it is the kth smallest element in the sorted order, not the kth distinct element.

## Example
Example1

Input:
matrix = [[ 1,  5,  9],[10, 11, 13],[12, 13, 15]]

k = 8

Output: 13

## 方法
sort函数进行排序的时间复杂度为n*log2n
build min heap 时间复杂度 logn


四种解法，第一，二种没有利用矩阵的性质，所以时间复杂度最差；第三种解法只利用了一部分性质（每一行是一个有序数列，而忽视了列之间的关系）；第四种解法则利用了全部性质，所以时间复杂度最佳。


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

# 方法3 归并k次的heap
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
# 方法4 二分法
时间复杂度：O(n\log(r-l))，二分查找进行次数为O(log(r−l))，每次操作时间复杂度为 O(n)
<img src="https://user-images.githubusercontent.com/60911066/152294319-081d2575-8d1d-42f4-b2e4-ef8f1be2bd11.png" width="50%" height="50%">

```
class Solution:
    def kthSmallest(self, matrix: List[List[int]], k: int) -> int:
        n = len(matrix)

        def check(mid):
            i, j = n - 1, 0
            num = 0
            while i >= 0 and j < n:
                if matrix[i][j] <= mid:
                    num += i + 1
                    j += 1
                else:
                    i -= 1
            return num >= k

        left, right = matrix[0][0], matrix[-1][-1]
        while left < right:
            mid = (left + right) // 2
            if check(mid):
                right = mid
            else:
                left = mid + 1
        
        return left

```
