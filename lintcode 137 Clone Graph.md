```
"""
class UndirectedGraphNode:
     def __init__(self, x):
         self.label = x
         self.neighbors = []
"""

class Solution:
    """
    @param node: A undirected graph node
    @return: A undirected graph node
    """
    def cloneGraph(self, node):
        if not node:
            return None
        
        # step 1: find nodes
        nodes = self.find_nodes_by_bfs(node)
        # step 2: copy nodes
        mapping = self.copy_nodes(nodes)
        # step 3: copy edges
        self.copy_edges(nodes, mapping)
        
        return mapping[node]
#BFS找到所有的点
    def find_nodes_by_bfs(self,node):
        queue = collections.deque([node])
        visited = set([node])
        while queue:
            cur_node = queue.popleft()
            for neighbor in cur_node.neighbors:
                if neighbor in visited:
                    continue
                queue.append(neighbor)
                visited.add(neighbor)
        return list(visited)

#复制所有的点
    def copy_nodes(self, nodes):
        mapping = {}
        for node in nodes:
            mapping[node] = UndirectedGraphNode(node.label)
        return mapping
#复制所有的边
    def copy_edges(self, nodes, mapping):
        for node in nodes:
            new_node = mapping[node]
            for neighbor in node.neighbors:
                new_neighbor = mapping[neighbor]
                new_node.neighbors.append(new_neighbor)


```
