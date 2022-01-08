二分法
```
class Solution:
    """
    @param nums: a list of integers
    @return: return a integer
    """
    def singleNonDuplicate(self, nums):
        lo = 0
        hi = len(nums) - 1   
        while lo < hi:
            mid = lo + (hi - lo) // 2
            halves_are_even = (hi - mid) % 2 == 0
            if nums[mid + 1] == nums[mid]:
                if halves_are_even:
                    lo = mid + 2
                else:
                    hi = mid - 1
            elif nums[mid - 1] == nums[mid]:
                if halves_are_even:
                    hi = mid - 2
                else:
                    lo = mid + 1
            else:
                return nums[mid]
        return nums[lo]

```
