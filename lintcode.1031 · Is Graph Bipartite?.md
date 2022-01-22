```
class Solution:
    """
    @param graph: the given undirected graph
    @return:  return true if and only if it is bipartite
    """
    def isBipartite(self, graph):
        n = len(graph)
        self.color = [0] * n
        for i in range(n):
            if self.color[i] == 0 and not self.colored(i, graph, 1):
                return False
        return True        
    
    def colored(self, now, graph, c):
        self.color[now] = c
        for nxt in graph[now]:
            if self.color[nxt] == 0 and not self.colored(nxt, graph, -c):
                return False
            elif self.color[nxt] == self.color[now]:
                return False
        return True
```
