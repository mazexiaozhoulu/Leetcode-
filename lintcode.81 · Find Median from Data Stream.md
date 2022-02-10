## Example 1:

Input:

add(1)
getMedian()
add(2)
getMedian()
add(3)
getMedian()
add(4)
getMedian()
add(5)
getMedian()
Output:

1
1
2
2
3
Explanation:

The median of [1] and [1,2] is 1,
The median of [1,2,3] and [1,2,3,4] is 2,
The median of [1,2,3,4,5] is 3.

## 方法：
两个heap，分别为lo, hi,
维持大小分配的条件：

lo存<=median 的数，为maxheap，
hi存>median的数，为minheap，
新来的数先从hi进，然后hi把最小给lo，即维持了分配的条件，
若lo数比hi多2个，再把lo的最大给hi，
所以lo的size 永远，

要么等于 hi，这时median为lo最大
要么比hi多一个，这时median也为lo最大
```
import heapq

class Solution:
    """
    @param nums: A list of integers
    @return: the median of numbers
    """
    def medianII(self, nums):
      # write your code here
      lo = []
      hi = []
      median = []
      for n in nums:
        heapq.heappush(lo, -heapq.heappushpop(hi, n))
        if len(lo) > len(hi) + 1:
          heapq.heappush(hi, -heapq.heappop(lo))
        median.append(-lo[0])
      return median
```
