```
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        n = len(nums)
        j = 0
        i = 0
        while j < n:

            if nums[j] != nums[i]:
                i+=1
                nums[i] = nums[j]
            j+=1

        return i + 1
            
```
