```
class Solution:
    """
    @param tasks: the given char array representing tasks CPU need to do
    @param n: the non-negative cooling interval
    @return: the least number of intervals the CPU will take to finish all the given tasks
    """
    def leastInterval(self, tasks, n):
        # write your code here
        #花花酱 讲解
        d = collections.Counter(tasks)
        counts = list(d.values())
        longest = max(counts)
        ans = (longest - 1) * (n + 1) + counts.count(longest)
        return max(len(tasks), ans)

```
