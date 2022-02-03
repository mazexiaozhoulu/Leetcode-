## Description
Return the length of the shortest, non-empty, contiguous subarray of A with sum at least K.

If there is no non-empty subarray with sum at least K, return -1.

## sample:
A = [72,-65,12,32,24,6,70]

K = 76


## 时间复杂度：
O(N) 其中 N 是数组 A 的长度。

## 方法

前缀和+deque滑动窗口

```
from collections import deque
class Solution:
    """
    @param A: the array
    @param K: sum
    @return: the length
    """
    def shortestSubarray(self, A, K):
        # Write your code here.
        #> 双指针 + deque[index,prefix]
        #> 如果下一个sum比当前sum小；就数值变小了，就把前一个pop出去
        d = deque([[-1,0]])
        result, prefix = float('inf'), 0
        for i,a in enumerate(A):
            prefix += a
        #如果满足条件（当前前缀和-start）>=k的话，就要把这一段放到result做对比
            while d and prefix - d[0][1] >= K:
                result = min(result, i - d[0][0])
        #做完对比后，开始滑动窗口，把开始的指针往后移动,只要poplet，指针就会自动右移
                d.popleft()
        # 如果当前前缀和 <= 已经在队列里的最后一个前缀和（就是前一个前缀和），说明当前的A[i] <=0；
        # 就要把最后一个前缀和从deque里pop掉，还是要当前的前缀和，因为需要知道=k的两个前缀和的长度
            while d and prefix <= d[-1][1]:
                d.pop()
            d.append([i,prefix])
        return result if result < float('inf') else -1

```
