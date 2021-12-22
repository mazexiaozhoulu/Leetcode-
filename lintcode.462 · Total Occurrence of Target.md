要注意找左边和右边时候 <= 和>=的区别
```
class Solution:
    """
    @param A: A an integer array sorted in ascending order
    @param target: An integer
    @return: An integer
    """
    def totalOccurrence(self, A, target):
        # write your code here
        if not A:
            return 0

        start = 0
        end = len(A)-1
        while start + 1 < end:
            mid = (start+end) // 2
            if A[mid] < target:
                start = mid
            elif A[mid] > target:
                end = mid
            else:
                end = mid

        if A[start] == target:
            first = start
        elif A[end] == target:
            first = end
        else:
            return 0

        start = 0
        end = len(A)-1
        while start + 1 < end:
            mid = (start+end) // 2
            if A[mid] <= target:
                start = mid
            else:
                end = mid

        if A[end] == target:
            last = end
        elif A[start] == target:
            last = start

        return last - first +1
```
