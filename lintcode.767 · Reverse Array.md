```
class Solution:
    """
    @param nums: a integer array
    @return: nothing
    """
    def reverseArray(self, nums):
        # write your code here
        for i in range(len(nums)//2):
            nums[i],nums[len(nums)-1-i] = nums[len(nums)-1-i],nums[i]
        return nums
```
