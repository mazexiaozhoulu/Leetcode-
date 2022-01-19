# Description
Reverse the given array nums inplace.
# Example 1:

Input:

interval list = [(1,2), (5,9)]

new interval = (2, 5)

Output:

[(1,9)]
#时间复杂度
时间复杂度：O(N)，其中 N 为字符数组的长度。一共执行了 N/2 次的交换。

# 代码
```
    def reverseArray(self, nums):
        # write your code here
        for i in range(len(nums)//2):
            nums[i],nums[len(nums)-1-i] = nums[len(nums)-1-i],nums[i]
        return nums
```

```
    def reverseArray(self, nums):
        if not nums:
            return None
        left = 0
        right = len(nums)-1
        while left < right:
            nums[left], nums[right] = nums[right], nums[left]
            left += 1
            right -= 1
        return nums
```
