三数之和，在两数之和 two points的方法基础上

需要注意的地方：

>流程逻辑
>sorted 和sort
>last_pair 检验
```
class Solution:
    """
    @param numbers: Give an array numbers of n integer
    @return: Find all unique triplets in the array which gives the sum of zero.
    """
    def threeSum(self, numbers):
        # write your code here
        nums = sorted(numbers)
        result = []
        for i in range(len(nums)):
            if i>0 and nums[i] == nums[i-1]:
                continue
            self.twosum(nums, i+1, len(nums)-1, -nums[i], result)
        return result

    def twosum(self, nums, left, right, target, result):
        last_pair = None
        while left < right:
            if nums[left] + nums[right] == target:
                if (nums[left], nums[right]) != last_pair:
                    result.append([-target, nums[left], nums[right]])
                last_pair = (nums[left], nums[right])
                right -= 1
                left += 1
            elif nums[left] + nums[right] < target:
                left += 1
            else:
                right -= 1
```
