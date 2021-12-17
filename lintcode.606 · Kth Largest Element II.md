建立负数最小堆，然后取最大值，再加负号还原
```
import heapq
class Solution:
    """
    @param nums: an integer unsorted array
    @param k: an integer from 1 to n
    @return: the kth largest element
    """
    def kthLargestElement2(self, nums, k):
        # write your code here
        self.heap = []
        for i in nums:
            heapq.heappush(self.heap, -i)

        result = []
        for _ in range(k):
            x = heapq.heappop(self.heap)
            result.append(x)
        return -result[k-1]

        

```
