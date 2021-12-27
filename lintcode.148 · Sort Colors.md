```
class Solution:
    """
    @param: nums: A list of integer which is 0, 1 or 2 
    @return: nothing
    """
    def sortColors(self, nums):
        # write your code here
        i = 0
        j = 0
        for n in range(len(nums)):
            v = nums[n]
            nums[n] = 2
            if v < 2:
                nums[j] = 1
                j += 1
            if v == 0:
                nums[i] = 0
                i += 1
```
```
class Solution:
    """
    @param nums: A list of integer which is 0, 1 or 2 
    @return: nothing
    """
    def sortColors(self, nums):
        self.partition_a(nums, 1)
        self.partition_a(nums, 2)
    
    def partition_a(self, num, k):
        last_small = -1
        for i in range(len(num)):
            if num[i] < k:
                last_small += 1
                num[last_small], num[i] = num[i], num[last_small]

        return last_small + 1
```
