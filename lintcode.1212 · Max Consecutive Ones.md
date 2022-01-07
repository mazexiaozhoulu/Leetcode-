```
    def findMaxConsecutiveOnes(self, nums):
        # Write your code here
        result = 0
        k = 0
        for i in nums:
            if i == 1:
                k += 1
            else:
                result=max(result, k)
                k = 0
        # 这个result 取max 是因为如果最后一个0之后的一组k是最大的，就需要做对比
        result = max(result, k)
        return result
```
