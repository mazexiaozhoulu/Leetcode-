## Description
Given an array of integers and an integer k, you need to find the minimum size of continuous no-empty subarrays whose sum equals to k, and return its length.

if there are no such subarray, return -1.

#Example
Example1

Input: 

nums = [2,1,-1,4,2,-3] and k = 3

Output: 

2

## Brute force 
O(N^3) - TLE
```
    def subarraySumEqualsKII(self, nums, k):
        # write your code here
        count = 0
        for i in range(len(nums)):
            for j in range(i, len(nums)):
                if sum(nums[i:j+1]) == k:
                    count += 1
        return count
```
## Prefix sum 
only works on positive nums
O(N^2) - TLE
```
    def subarraySumEqualsKII(self, nums, k):
        # write your code here
        # 思路： 
        # 1: 先做个prefix的list，用enumerate返回各个index的prefixsum
        # 2: 在dict里找到差值为k的两个数，返回这两个数的index
        result = []
        sum = 0
        for i in range(len(nums)):
            sum += nums[i]
            result.append(sum)

        size = float("inf")
        for index1, value1 in enumerate(result):
            for index2, value2 in enumerate(result):
                if value2 + k == value1:
                    size = min(index1 - index2, size)
        return size
```
## 使用 prefix+hash 的方法
```
        if not nums:
            return -1

        subSum = {0: -1}
        rightSum = 0
        less = float('inf')
        for rightIdx, num in enumerate(nums):
            rightSum += num
            leftSum = rightSum - k

            if leftSum in subSum:
                leftIdx = subSum[leftSum]
                less = min(less, rightIdx - leftIdx)
                # print(leftIdx, rightIdx)
            
            subSum[rightSum] = rightIdx
        
        return -1 if less == float('inf') else less
```
