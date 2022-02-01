## Description
Given an array of n positive integers and a positive integer s, find the minimal length of a subarray of which the sum ≥ s. If there isn't one, return -1 instead.

## Example
Example 1:

Input: [2,3,1,2,4,3], s = 7

Output: 2

Explanation: The subarray [4,3] has the minimal length under the problem constraint.

## 方法1:brute force 

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
## 方法2:优化1: prefix sum 
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

比o(n^2)还要好的情况就是 

>o(nlogn);

[可选：n次二分法(nums都是正整数)：(确定起点或终点，再用二分法确定另一个点)对于每个下标i，都让它作为子数组的左边界，使用二分法找到子数组最靠左的右边界，使用前缀和求出子数组之和，与s比较更新答案]

[不可选：排序（破坏子数组顺序）]

[不可选：heap(但可能需要其他的操作，最终到不了logn)]

[不可选：n次快速幂算法；求最大公约数]

>o(n * sqrt(n)); [因子(factor)相关问题]

>o(n)；[双指针；单调栈；quick select；树上各类遍历分治；n次并查集操作；n次哈希表]

## 方法3:优化2
n次二分法 o(nlogn)

```
class Solution:
    """
    @param nums: an array of integers
    @param s: An integer
    @return: an integer representing the minimum size of subarray
    """
    def minimumSize(self, nums, s):
        # write your code here
        n = len(nums)
        min_length = float('inf')
        prefix_sum = self.get_prefix_sum(nums)
        for start in range(n):
            end = self.get_end_of_subarray(prefix_sum, start, s)
            if prefix_sum[end+1]-prefix_sum[start] >= s:
                min_length = min(min_length, end-start+1)
        
        if min_length == float('inf'):
            return -1
        return min_length

    def get_end_of_subarray(self, prefix_sum,start,s):
        left,right = start, len(prefix_sum)-2
        while left+1<right:
            mid = left + (right - left) // 2
            if prefix_sum[mid+1] - prefix_sum[start] >= s:
                right = mid
            else:
                left = mid
        if prefix_sum[left+1] - prefix_sum[start] >= s:
            return left
        return right

    def get_prefix_sum(self, nums):
        prefix_sum = [0]
        for i in range(1, len(nums)+1):
            prefix_sum.append(prefix_sum[i-1]+nums[i-1])
        return prefix_sum
```

双指针：

> 同向：全零子串数量

> 相向：两数之和，三数之和

> 背向：最长回文子串

## 方法4:优化3 
时间复杂度o(n + n ) = o(n)

同向双指针
![10491643741958_ pic](https://user-images.githubusercontent.com/60911066/152033181-cfe5125a-705b-4d90-b774-5bf0f97ccbd0.jpg)
```
    def minimumSize(self, nums, s):
        # write your code here
        if not nums:
            return -1

        n = len(nums)
        j = 0
        sum_of_array = 0
        min_length = float("inf")

        for i in range(n):
            while j < n and sum_of_array < s:
                sum_of_array += nums[j]
                j += 1
            if sum_of_array >= s:
                min_length = min(j-i, min_length)
            sum_of_array -= nums[i]

        if min_length == float('inf'):
            return -1
        return min_length
```
