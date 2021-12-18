dict 和 heap的交叉应用
要理清 loop 下的dict
```
import heapq
from collections import defaultdict
'''
Definition for a Record
class Record:
    def __init__(self, id, score):
        self.id = id
        self.score = score
'''
class Solution:
    # @param {Record[]} results a list of <student_id, score>
    # @return {dict(id, average)} find the average of 5 highest scores for each person
    # <key, value> (student_id, average_score)
    def highFive(self, results):
        # Write your code here
        scores = defaultdict(list)
        for Record in results:
            heapq.heappush(scores[Record.id], Record.score)
            if len(scores[Record.id]) > 5:
                heapq.heappop(scores[Record.id])
        
        avg_score = {}
        for id in scores:
            avg_score[id] = sum(scores[id]) / 5.0
        return avg_score
```
