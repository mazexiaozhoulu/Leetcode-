#1: 在two sum的基础上
```
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        hash = set()
        for idx in range(len(nums)):
            if nums[idx] not in hash:
                hash.add(target - nums[idx])
            else:
                return nums.index(target-nums[idx]),idx
```
用一个set把成立的数值去重存起来。在计算这个set的长度
```
class Solution:
    """
    @param nums: an array of integer
    @param target: An integer
    @return: An integer
    """
    def twoSum6(self, nums, target):
        # write your code here
        # output = 0
        lis = set()
        store = set()
        for num in nums:
            if num not in store:
                store.add(target - num)
            else:
                lis.add(num)
        return len(lis)

```
