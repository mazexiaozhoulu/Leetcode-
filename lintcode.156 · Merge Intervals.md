```
class Solution:
    
    def merge(self, intervals):
        
        if not intervals: return []
        
        intervals = sorted(intervals, key = lambda interval: interval.start)
        
        last, output = None, []
        for interval in intervals:
            if not last or last.end < interval.start:
                output.append(interval)
                last = interval
            else:
                last.end = max(last.end, interval.end)
                
        return output
```
