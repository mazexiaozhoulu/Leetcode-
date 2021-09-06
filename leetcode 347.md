347. Top K Frequent Elements

collections import Counter用于统计数量

most_common用于找出value值最多的key

再用for loop 输出key
```
from collections import Counter
class Solution(object):
    def topKFrequent(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: List[int]
        """
        if k == len(nums):
            return nums
        
        count = (Counter(nums).most_common(k))
        return(i[0] for i in count)
```
