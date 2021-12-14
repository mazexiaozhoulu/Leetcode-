回溯
```
class Solution:
    """
    @param nums: A set of numbers
    @return: A list of lists
    """
    def subsets(self, nums):
        # write your code here
        result = []
        if not nums:
            return [[]]
        if len(nums) == 0:
            return [[]]

        nums.sort()
        self.dfs(nums, 0, [], result)
        return result

    def dfs(self, nums, index, subset, results):
        results.append(subset[:])
        for i in range(index, len(nums)):
            subset.append(nums[i])
            self.dfs(nums, i+1, subset, results)
            subset.pop(-1) #backtracking
```
