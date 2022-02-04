>起点是1
>终点是max(L)
>对每个小段的长度进行二分搜索
```
class Solution:
    """
    @param L: Given n pieces of wood with length L[i]
    @param k: An integer
    @return: The maximum length of the small pieces
    """
    def woodCut(self, L, k):
        # write your code here
        if not L or not k:
            return 0

        start = 1
        # end 要用max(L), 因为不一定是所有pieces of wood 都要用上，如果这个木棍太小，用不上，但count>=k 也可以
        end = max(L)

        while start + 1 < end:
            length = (start+end) // 2
            if self.get_amount(L,length) < k:
                end = length
            else:
                start = length
        
        if self.get_amount(L,end) >= k:
            return end
        if self.get_amount(L,start) >=k:
            return start
        return 0


    def get_amount(self, L, length):
        count = 0
        for l in L:
            count += (l // length)
        return count
```
