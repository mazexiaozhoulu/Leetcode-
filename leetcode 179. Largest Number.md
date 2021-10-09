中心思想，变成str的两个数字a,b合并变成一个数字ab或ba，如果ab小，就调换ab的位置。
flag的作用是记录是否还有交换。
时间复杂度:o(n^2)
空间复杂度：o(n)
```
class Solution(object):
    def largestNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: str
        """
        
        str_nums=[]
        for i in nums:
            str_nums.append(str(i))
            
        str_nums.sort(reverse=True) // 减少时间复杂度
        
        flag = False
        while not flag:
            j = 0
            flag = True
            while j < len(str_nums)-1:
                if str_nums[j] + str_nums[j+1] < str_nums[j+1] + str_nums[j]:
                    str_nums[j],str_nums[j+1] = str_nums[j+1],str_nums[j]
                    flag = False
                j += 1
        res = "".join(str_nums)
        if res[0]=="0":
            return str(0)
        
        return res
            
```
