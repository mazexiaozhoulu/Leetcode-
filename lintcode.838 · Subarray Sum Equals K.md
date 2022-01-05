# first we start from a sum which is equal to 0, and the count of it is 1. 
# this is the input list ex :    [   1    4    9     -5   8]
# this is the sum array (s) ex : [0  1    5    13    8    16 ]    
# sumDict key: sum; value: # of occurance
# sumDict:{[0:1, 1:1, 5:1, 13:1, 8:1, 16:1]}

如果[1,2,5,-5] k = 5

那dict = {0: 1, 1: 1, 3: 2, 8: 1}

count = 1

不会出现count=2的结果，因为统计到8的时候，3只有一个。所以count=1；最后一个3是在-5之后才出现的，那个时候的sum = 3； 3-5=-2不在dict里。
```
class Solution:
    """
    @param nums: a list of integer
    @param k: an integer
    @return: return an integer, denote the number of continuous subarrays whose sum equals to k
    """

    def subarraySum(self, nums: List[int], k: int) -> int:
    
        sumDict = {0:1}
        n = len(nums)
        count = 0 
        sum = 0 
    
        for num in nums:
#we keep adding to the cumilative sums, s; 计算前缀和        
            sum += num

#we make sure to check if the sum - k is already in the dictionary, if so, increase the count.： 
#如果 sum - k （就是sumDict的key）出现了，就在count里增加出现的次数（key的value）
            if sum-k in sumDict:
                count += sumDict[s-k]

# #we check if s is already in the sumDict, if so, increase by 1, if not assign 1.             
            if sum in sumDict:
                sumDict[s] +=1
            else:
                sumDict[s] = 1

#finally return the occurance    
        return count
```
