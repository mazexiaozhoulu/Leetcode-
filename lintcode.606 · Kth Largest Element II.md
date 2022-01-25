# Description
Find K-th largest element in an array, and N is much larger than k. Note that it is the kth largest element in the sorted order, not the kth distinct element.

# Example
Example 1:

Input:[9,3,2,4,8],3
Output:4
Example 2:

Input:[1,2,3,4,5,6,8,9,10,7],10
Output:1

#
O(n + klogn) 建立负数最小堆，然后取最大值，再加负号还原
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
