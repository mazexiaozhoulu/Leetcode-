双指针算法
```
#双指针
class Solution(object):
    def twoSum(self, nums, target):
        #时间复杂度：o(nlogn)；空间复杂度o(n)
        if nums is None:
            return [-1, -1]
        
        numbers = []
        for index, number in enumerate(nums):
            # enumerate format[(index, number)...]
            numbers.append((number,index))
        print(numbers)
        numbers.sort()#sort的作用是让list根据数字大小排序，而不是index大小
        print(numbers)
        
        left, right = 0, len(nums)-1
        while left < right:
            if numbers[left][0] + numbers[right][0] > target: 
                #numbers[left][0]指的是left指标指向（2，0），[0]指向(2，0)里的第一个2，数字
                right -= 1
            elif numbers[left][0] + numbers[right][0] < target:
                left += 1
            else:
                return sorted([numbers[left][1], numbers[right][1]])
                #numbers[left][1]指的是left指标指向（2，0），[1]指向(2，0)里的第二个0，下标
            
        return [-1,-1]
```
Hashmap算法
```
class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        hash = {}
        for i in range(len(nums)):
            if target - nums[i] in hash:
                return [hash[target-nums[i]], i]
            hash[nums[i]] = i
            
        return [-1, -1]
```
