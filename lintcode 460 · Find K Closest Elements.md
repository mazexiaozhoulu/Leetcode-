```
class Solution:
    """
    @param A: an integer array
    @param target: An integer
    @param k: An integer
    @return: an integer array
    """
    def kClosestNumbers(self, A, target, k):
        # write your code here
        right = self.binary(A, target)
        left = right -1

        result = []
        for _ in range(k):
            if left < 0:
                result.append(A[right])
                right +=1
            elif right == len(A):
                result.append(A[left])
                left -=1
            else:
                if target - A[left] <= A[right] - target:
                    result.append(A[left])
                    left -= 1
                else:
                    result.append(A[right])
                    right += 1

        return result
# 找到 >= target的最左数字（比如在1，2，4，6，8里找3的位置，那我们就要找出来right 为4的位置,返回到上一层，left是right-1 就是2）
    def binary(self, A, target):
        start, end = 0, len(A)-1
        while start + 1 < end:
            mid = (end + start)//2
            if A[mid] < target:
                start = mid
            elif A[mid] > target:
                end = mid
            else:
                end = mid
        
        if A[start] >= target:
            return start
        if A[end] >= target:
            return end
        return len(A)
```
