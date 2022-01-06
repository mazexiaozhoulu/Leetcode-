前缀和+滑动窗口
```
from collections import deque
class Solution:
    """
    @param A: the array
    @param K: sum
    @return: the length
    """
 #   [84, -37, 32,40,95]
 #   k = 167
    def shortestSubarray(self, A, K):
        d = collections.deque([[0, 0]])
        res, cur = float('inf'), 0
        for i, a in enumerate(A):
            cur += a
            #d存在，并且现在的前缀和-第一个前缀和（就是第一个数字）>=k；
            while d and cur - d[0][1] >= K:
                #res = min(res, l-r+1)
                #d.popleft()[0]就是d这个queue，popleft出去第一个元素，[0]就是第一个元素的0index
                #popleft就是缩小左边界，去找下一个满足的subarray
                res = min(res, i+1 - d.popleft()[0])
            # cur<=前一个，就说明现在的sum变小了，所以要把前一个pop出去。
            while d and cur <= d[-1][1]:
                d.pop()
            d.append([i+1, cur])
            #
        return res if res < float('inf') else -1

```
