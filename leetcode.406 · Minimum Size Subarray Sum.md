## Description
Given an array of n positive integers and a positive integer s, find the minimal length of a subarray of which the sum ≥ s. If there isn't one, return -1 instead.

## Example
Example 1:

Input: [2,3,1,2,4,3], s = 7

Output: 2

Explanation: The subarray [4,3] has the minimal length under the problem constraint.

## brute force 

> 三重循环，循环1:找start
> 循环2:在start之后循环一个end
> 循环3:在start和end之间找 出来sum，做对比

时间复杂度o(n^3) & 空间复杂的o(1)
```
class Solution:
    """
    @param nums: an array of integers
    @param s: An integer
    @return: an integer representing the minimum size of subarray
    """
    def minimumSize(self, nums, s):
        # write your code here
        result = float('inf')
        for start in range(len(nums)):
            for end in range(start, len(nums)):
                sum_of_subsrray = 0
                for i in range(start, end+1):
                    sum_of_subsrray += nums[i]
                if sum_of_subsrray >= s:
                    result = min(result, end - start + 1)

        if result == float('inf'):
            return -1
        else:
            return result

```
## prefix sum improve
时间复杂度o(n^2)&空间复杂度o(n)

> 两重循环，循环1:找start
> 循环2:在start之后循环一个end
> 用prefixsum找到sum


```
    def minimumSize(self, nums, s):
        # write your code here
        n = len(nums)
        min_length = float('inf')
        prefix_sum = self.get_prefix_sum(nums)
        for start in range(n):
            for end in range(n):
                if prefix_sum[end+1] - prefix_sum[start] >= s:
                    min_length = min(min_length, end - start + 1)

        if min_length == float('inf'):
            return -1
        else:
            return min_length

    def get_prefix_sum(self, nums):
        prefix_sum = [0]
        for i in range(1, len(nums)+1):
            prefix_sum.append(prefix_sum[i-1] + nums[i-1])
        return prefix_sum
```
