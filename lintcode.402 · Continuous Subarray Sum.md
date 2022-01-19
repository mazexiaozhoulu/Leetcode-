# Description
Given an integer array, find a continuous subarray where the sum of numbers is the biggest. Your code should return the index of the first number and the index of the last number. (If their are duplicate answer, return the minimum one in lexicographical order)
# Example
Example 1:

Input: [-3, 1, 3, -3, 4]

Output: [1, 4]

Example 2:

Input: [0, 1, 0, 1]

Output: [0, 3]

Explanation: The minimum one in lexicographical order.
# 思路
        # max_sum维护全局最大连续子数组和
        # sum维护当前最大连续子数组和，即当前元素必选的最大和
        # first, last表示全局最大连续子数组的左右端点
        # bg表示当前连续子数组的左端点
# 复杂度
空间复杂度O(1)
时间复杂度O(n)

# 代码
```
class Solution:
    """
    @param: A: An integer array
    @return: A list of integers includes the index of the first number and the index of the last number
    """
    def continuousSubarraySum(self, A):
        n = len(A)

        max_sum = A[0]
        sum = 0
        first = last = 0
        bg = 0;
        for i in range(n):
            if sum >= 0:
                sum += A[i]
            else:
                bg = i
                sum = A[i]
            if max_sum < sum:
                print(max_sum)
                max_sum = sum
                first = bg
                last = i
        return [first,last]
```
