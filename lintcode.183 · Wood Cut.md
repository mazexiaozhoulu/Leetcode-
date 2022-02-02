>起点是最短木棒//k
>终点是总长度//k
>对小段的长度进行二分搜索
```
    def woodCut(self, L, k):
        # write your code here
        if not L or k <= 0:
            return 0 
        
        start, end = 1, max(L)
        while start + 1 < end:
            mid = (start + end) // 2
            if self.get_pieces(mid, L) < k:
                end = mid  
            else:
                start = mid 
        #看哪个情况成立就返回哪个
        if self.get_pieces(end, L) >= k:
            return end 
        if self.get_pieces(start, L) >= k:
            return start 
        return 0
    
    def get_pieces(self, length, L):
        count = 0
        for l in L:
            count += (l // length) 
        return count
```
