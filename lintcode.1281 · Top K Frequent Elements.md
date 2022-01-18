
时间复杂度o(nlogn)
```
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        hashmap = {}
        for num in nums:
            if num in hashmap:
                hashmap[num] += 1
            else:
                hashmap[num] = 1
        heap = []
        for key in hashmap:
            heapq.heappush(heap, (-hashmap[key], key))
        
        res = []
        for _ in range(k):
            topk = heapq.heappop(heap)
            res.append(topk[1])
        
        return res
```

时间复杂度 O(n)
```
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        # 桶排序
        bucket = [[] for i in range(len(nums)+1)]
        res = []
        freq = collections.Counter(nums)
        for key, val in freq.items():  # key为数字，val为这个数字出现的次数
            bucket[val].append(key)

        for i in range(len(bucket)-1, -1, -1):  # 从大往小找
            if len(bucket[i]): res += bucket[i]
            if len(res) >= k: return res[0:k]
```
