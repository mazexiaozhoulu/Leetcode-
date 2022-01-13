same as lintcode402
```
class Solution:
    """
    @param nums: A list of integers
    @return: A integer indicate the sum of max subarray
    """
    def maxSubArray(self, A):
        # write your code here
        n = len(A)
        # max_sum维护全局最大连续子数组和
        # sum维护当前最大连续子数组和，即当前元素必选的最大和
        max_sum = A[0]
        sum = 0
        for i in range(n):
            #第一个if else 是用来遍历所有数字，并且
            if sum >= 0:
                sum += A[i]
            else:
                sum = A[i]

            if max_sum < sum:
                max_sum = sum
        return max_sum
```
