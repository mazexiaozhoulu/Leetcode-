用flag，速度比较慢，最好先用sort一下减少时间复杂度。
时间复杂度o(n^2)
```
class Solution(object):
    def sortColors(self, nums):
        """
        :type nums: List[int]
        :rtype: None Do not return anything, modify nums in-place instead.
        """
        flag = False
        while not flag:
            i = 0
            flag = True
            while i < len(nums)-1:
                if nums[i] > nums[i+1]:
                    nums[i], nums[i+1] = nums[i+1], nums[i]
                    flag = False
                i += 1
        return nums
```
或者用双指针O（n）
```
class Solution(object):
    def sortColors(self, nums):
        """
        :type nums: List[int]
        :rtype: None Do not return anything, modify nums in-place instead.
        """
        for i in range(len(nums)-1):
            for j in range(i+1,len(nums)):
                if nums[i]>nums[j]:
                    # print(i)
                    nums[i],nums[j]=nums[j],nums[i]
```
