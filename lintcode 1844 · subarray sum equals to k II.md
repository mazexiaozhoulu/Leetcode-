## Brute force 
O(N^3) - TLE
```
    def subarraySumEqualsKII(self, nums, k):
        # write your code here
        count = 0
        for i in range(len(nums)):
            for j in range(i, len(nums)):
                if sum(nums[i:j+1]) == k:
                    count += 1
        return count
```
## Prefix sum 

O(N^2) - TLE
```
    def subarraySumEqualsKII(self, nums, k):
        # write your code here
        # 思路： 
        # 1: 先做个prefix的list，用enumerate返回各个index的prefixsum
        # 2: 在dict里找到差值为k的两个数，返回这两个数的index
        result = []
        sum = 0
        for i in range(len(nums)):
            sum += nums[i]
            result.append(sum)

        size = float("inf")
        for index1, value1 in enumerate(result):
            for index2, value2 in enumerate(result):
                if value2 + k == value1:
                    size = min(index1 - index2, size)
        return size
```
## Prefix hashmap 

O(N) - [Accepted]

Single scan. Given the current sum and the k, we check if (sum-k) existsed before at an earlier stage (at a smaller window size)
```
def subarraySum(self, nums: List[int], k: int) -> int:
       d = {}
       d[0] = 1
       s = 0
       count = 0
       for i in range(len(nums)):
           s += nums[i]
           if s-k in d: # --- I
               count += d[s-k]
               # or return True
               # or return indicies
           
           # add sum to frq dict
           if s in d:
               d[s] += 1 # --- II
           else:
               d[s] = 1
       
       return count
```
