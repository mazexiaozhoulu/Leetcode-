基于17题，sorting nums 后，在每次for loop的时候查一下，现在的数字是不是和上一位相同
```
class Solution:
    """
    @param nums: A set of numbers.
    @return: A list of lists. All valid subsets.
    """
    def subsetsWithDup(self, nums):
        # write your code here
        if not nums:
            return [[]]
        if len(nums) == 0:
            return [[]]

        result = []
        nums.sort()
        self.dfs(nums, 0, [], result)
        return result

    def dfs(self, nums, index, subsets, results):
        results.append(subsets[:])
        for i in range(index, len(nums)):
            if (i != 0 and nums[i] == nums[i-1] and i > index):
                continue
            subsets.append(nums[i])
            self.dfs(nums, i+1, subsets, results)
            subsets.pop(-1)
```
