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
## 优化1: prefix sum 
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
## 优化2

比o(n^2)还要好的情况就是 
>o(nlogn);
[可选：n次二分法(确定起点或终点，再用二分法确定另一个点)；
不可选：排序（破坏子数组顺序）；
heap(但可能需要其他的操作，最终到不了logn)；
n次快速幂算法；求最大公约数]

>o(n * sqrt(n)); [因子(factor)相关问题]

>o(n)；[双指针；单调栈；quick select；树上各类遍历分治；n次并查集操作；n次哈希表]
