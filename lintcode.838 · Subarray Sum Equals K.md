```
class Solution:
    """
    @param nums: a list of integer
    @param k: an integer
    @return: return an integer, denote the number of continuous subarrays whose sum equals to k
    """

    def subarraySumEqualsK(self, nums, k):
        # write your code here
        for i in range(1, len(nums)):
        	nums[i] += nums[i - 1]
        d, ans = {0 : 1}, 0
        for i in range(len(nums)):
        	if(d.get(nums[i] - k) != None):
        		ans += d[nums[i] - k]
        	if(d.get(nums[i]) == None):
        		d[nums[i]] = 1
        	else:
        		d[nums[i]] += 1
        return ans
```
