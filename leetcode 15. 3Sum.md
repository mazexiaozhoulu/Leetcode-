用2sum 去解3sum
```
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        nums = sorted(nums)
        result = [] 
        for i in range(len(nums)):
            if i > 0 and nums[i] == nums[i-1]:
                continue
            self.twosum(nums, i+1, len(nums)-1, -nums[i], result)
        return result
            
    def twosum(self, nums, left, right, target, result):
        last_pair = None
        while left < right:
            if nums[left] + nums[right] == target:
                if (nums[left], nums[right]) != last_pair:
                    result.append([-target, nums[right], nums[left]])
                last_pair = (nums[left], nums[right])
                right -= 1
                left += 1
            elif nums[left] + nums[right] > target:
                right -= 1
            else:
                left += 1
```
