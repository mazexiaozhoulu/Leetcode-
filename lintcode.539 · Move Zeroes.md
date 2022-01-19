# Description
Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.
# Example 1:

Input: nums = [0, 1, 0, 3, 12],

Output: [1, 3, 12, 0, 0].

# 思路1:双指针
时间复杂度O（n）
空间复杂度O（1）

```
class Solution:
    def moveZeroes(self, nums):
        n = len(nums)
        left = right = 0
        while right < n:
            if nums[right] != 0:
                nums[left], nums[right] = nums[right], nums[left]
                left += 1
            right += 1
```
# 思路2：逆向遍历，覆盖如果为0就在后面加个0，并且把当前的0 delete


```
        for i in range(len(nums)-1,-1,-1):
            if nums[i]==0:
                nums.append(0)
                del nums[i]
        return nums
```
