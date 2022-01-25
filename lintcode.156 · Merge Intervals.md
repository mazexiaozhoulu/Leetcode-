# Description
Given a collection of intervals, merge all overlapping intervals.

# Example 2:

Input:  [(1,3),(2,6),(8,10),(15,18)]
Output: [(1,6),(8,10),(15,18)]

# time 
O(n log n) time and O(1) extra space.
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
