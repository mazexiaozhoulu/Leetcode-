## Description
Given an array of integers and an integer k, you need to find the minimum size of continuous no-empty subarrays whose sum equals to k, and return its length.

if there are no such subarray, return -1.

## Example
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
    def subarraySumEqualsKII(self, nums, k):
        prefix_sum = self.get_prefix_sum(nums)
        
        answer = float('inf')
        sum2index = {0: 0}
        for end in range(len(nums)):
        
            ## find prefix_sum[end + 1] - prefix_sum[start] = k
            ## => prefix_sum[start] = prefix_sum[end + 1] - k
            
            if prefix_sum[end + 1] - k in sum2index:
               length = end + 1 - sum2index[prefix_sum[end + 1] - k] 
               answer = min(answer, length)
            #因为我们是从end往前计算长度，所以我们遇到更靠近end的start时，就要更新start的位置
            sum2index[prefix_sum[end + 1]] = end + 1
            
        return -1 if answer == float('inf') else answer
        
    def get_prefix_sum(self, nums):
        prefix_sum = [0]
        for num in nums:
            prefix_sum.append(prefix_sum[-1] + num)
        return prefix_sum
```
