想用 快速排序算法的双向双指针，但做出来的答案就不对了
Input Data
[0,1,0,3,12]
Output Data
[12,1,3,0,0]
Expected
[1,3,12,0,0]
```
class Solution:
    """
    @param nums: an integer array
    @return: nothing
    """
    def moveZeroes(self, nums):
        # write your code here
        left, right = 0, len(nums)-1
        while left <= right:
            while left <= right and nums[left] > 0:
                left += 1
            while left <= right and nums[right] == 0:
                right -= 1
            if left <= right and nums[left] == 0 and nums[right] !=0:
                nums[left], nums[right] = nums[right], nums[left]
                left += 1
                right -= 1
        return left
```
