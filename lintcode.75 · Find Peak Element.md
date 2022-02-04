```
class Solution:
    """
    @param: A: An integers array.
    @return: return any of peek positions.
    """
    def findPeak(self, A):
        # write your code here
        if len(A) == 0:
            return -1
        start = 0
        end = len(A) - 2
        while start + 1 < end:
            mid = start + (end - start) // 2
            if A[mid] < A[mid+1]:
                #如果mid<mid+1,那么是上升，所以峰值再后面，所以mid变成新的start
                start = mid
            else:
                #如果mid > mid+1,那么是下降，所以峰值在前面，所以mid变成新的end
                end = mid
                
        if A[start] > A[end]:
            return start
        else:
            return end
```
