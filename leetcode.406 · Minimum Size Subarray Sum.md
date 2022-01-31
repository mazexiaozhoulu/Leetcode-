## brute force 
o(n^3)
```
class Solution:
    """
    @param nums: an array of integers
    @param s: An integer
    @return: an integer representing the minimum size of subarray
    """
    def minimumSize(self, nums, s):
        # write your code here
        result = float('inf')
        for start in range(len(nums)):
            for end in range(start, len(nums)):
                sum_of_subsrray = 0
                for i in range(start, end+1):
                    sum_of_subsrray += nums[i]
                if sum_of_subsrray >= s:
                    result = min(result, end - start + 1)

        if result == float('inf'):
            return -1
        else:
            return result

```
