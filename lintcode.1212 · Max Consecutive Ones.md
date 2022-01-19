# Description
Given a binary array, find the maximum number of consecutive 1s in this array.

# sample
Input: [1,1,0,1,1,1]
Output: 3
Explanation: The first two digits or the last three digits are consecutive 1s.
    The maximum number of consecutive 1s is 3.

# 时间复杂度
Time Complexity: O(N)

# 代码
```
    def findMaxConsecutiveOnes(self, nums):
        # Write your code here
        result = 0
        k = 0
        for i in nums:
            if i == 1:
                k += 1
            else:
            #取到0的时候，说明当前的连续1断了，要给k做个结束，所以需要把当前最大值保存下来
                result=max(result, k)
                k = 0
        # 这个result 取max 是因为如果最后一个0之后的一组k是最大的，就需要做对比
        result = max(result, k)
        return result
```
