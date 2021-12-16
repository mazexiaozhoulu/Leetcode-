```
class Solution:
    """
    @param nums: a continuous stream of numbers
    @param number: a number
    @return: returns the first unique number
    """
    def firstUniqueNumber(self, nums, number):
        # Write your code here
        if not nums:
            return -1
        
        counter = {}
        for num in nums:
            counter[num] = counter.get(num,0)+1
            if num == number:
                break
        else:
            return -1
        
        for num in nums:
            if counter[num] == 1:
                return num
            if num == number:
                break

        return -1
```
