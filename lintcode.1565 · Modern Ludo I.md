## 方法1 BFS+BFS

时间复杂度 0(m+n)

        #思路
        
        #>一个bfs找最短路径
        
        #>一个bfs做一个连通块
        
        #1:先把connection做一个hashset的图,每个点的distance用hashamp
        
        #2:get_unvisited_node函数用BFS做连通块把当前node的neighbor和neighbor的connection neighbors找出来（如果已经在distance里就跳过）
        
        #3:主函数：将unvisited过（不在distance里）的connection neighbor,用bfs找到最短路径，存到distance里
        
```
class Solution:
    """
    @param length: the length of board
    @param connections: the connections of the positions
    @return: the minimum steps to reach the end
    """
    def modernLudo(self, length, connections):
        from collections import deque
        graph = self.build_graph(length, connections)
        queue = deque([1])
        distance = {1:0}
        while queue:
            node = queue.popleft()
            # neighbor的范围是:当前节点的下一位 直到 骰子1-6之间的所有可能性（如果超出length的范围就不算）
            #比如node 1 的neighbor 就是2，3，4，5，6，7
            #比如node 6 的neighbor 就是7，8，9，10
            for neighbor in range(node + 1, min(node + 7, length + 1)):
                #connection_nodes是在graph中neighbor连通的所有节点都找到，在这个过程中会把distance的节点传进去
                #比如：neighbor为2 connection_nodes就是{2, 10}
                connection_nodes = self.get_unvisited_node(graph, distance, neighbor)
                # 记录connection_nodes里每个connection_node到node 的distance
                # 比如 node 1 的neighbor是2，2的connection_nodes就是{2，10}
                # 所以 2 到 1 的 distance 是1， 10到 1 的 distance 是1
                for connection_node in connection_nodes:
                # node,neighbor,connection_nodes,distance[connection_node],queue 1 2 {2, 10} 1 deque([2])
                # node,neighbor,connection_nodes,distance[connection_node],queue 1 2 {2, 10} 1 deque([2, 10])
                    distance[connection_node] = distance[node] + 1
                    queue.append(connection_node)
        return distance[length]
    
    def build_graph(self, length, connections):
        graph = {
            i: set()
            for i in range(1, length+1)
        }
        for a, b in connections:
            #有向边
            graph[a].add(b)
        return graph

    def get_unvisited_node(self, graph, distance, node):
        from collections import deque
        queue = deque([node])
        unvisited_nodes = set()
        while queue:
            node = queue.popleft()
            #如果这个node已经在distance里了，就跳过找下一个
            #比如10， 10在2的graph已经出现过，distance为1；如果10在4的graph还需要计算，distance为1的话，就增加复杂度了
            if node in distance:
                continue
            unvisited_nodes.add(node)
            for neighbor in graph[node]:
                if neighbor not in distance:
                    queue.append(neighbor)
                    unvisited_nodes.add(neighbor)
        return unvisited_nodes

```
## 方法2 交替两个queue
```
class Solution:
    """
    @param length: the length of board
    @param connections: the connections of the positions
    @return: the minimum steps to reach the end
    """
    def modernLudo(self, length, connections):
        # Write your code here
        graph = self.build_graph(length, connections)
# 先把direct_node都找出来，同层扩展，连通扩展
        queue = [1]
        distance = {1:0}
        while queue:
            next_queue = []
            for node in queue:
                for direct_node in graph[node]:
                    if direct_node in distance:
                        continue
                    distance[direct_node] = distance[node]
                    queue.append(direct_node)
#最短路径bfs, 在distance里每个key，最先保存的value就是value就是最短路径
            for node in queue:
                for next_node in range(node + 1, min(node+7,length+1)):
                    if next_node in distance:
                        continue
                     #扔骰子扔出来的结果，所以distance+1
                    distance[next_node] = distance[node] + 1
                    next_queue.append(next_node)
            queue = next_queue
        return distance[length]
            
    def build_graph(self, length, connections):
        graph = {
            i: set()
            for i in range(1, length+1)
        }
        for a, b in connections:
            #有向边
            graph[a].add(b)
        return graph
```
## 方法3 spfa最短路径算法
<img src="https://user-images.githubusercontent.com/60911066/152661954-a5bb86e9-466a-472f-ac85-636e6a0d4e32.png" width="40%" height="40%"> 

<img src="https://user-images.githubusercontent.com/60911066/152661979-53cb3d4f-2ab6-4b88-8381-e2e4c23bca96.png" width="40%" height="40%"> 

```
class Solution:
    def modernLudo(self, length, connections):
        from collections import deque
        graph = self.build_graph(length, connections)
        
        queue = deque([1])
        distance = {
            i: float('inf')
            for i in range(1, length + 1)
        }
        distance[1] = 0
        while queue:
            node = queue.popleft()
            for next_node in graph[node]:
                if distance[next_node] > distance[node]:
                    distance[next_node] = distance[node]
                    queue.append(next_node)
            for next_node in range(node + 1, min(node + 7, length + 1)):
                if distance[next_node] > distance[node] + 1:
                    distance[next_node] = distance[node] + 1
                    queue.append(next_node)
        return distance[length]

    def build_graph(self, length, connections):
        graph = {
            i: set()
            for i in range(1, length + 1)
        }
        for a, b in connections:
            graph[a].add(b)
        return graph
        
  
```
## 方法4， spfa的heap优化
```
class Solution:
    def modernLudo(self, length, connections):
        import heapq

        graph = self.build_graph(length, connections)
        queue = [(0, 1)]
        distance = {
            i: float('inf')
            for i in range(1, length + 1)
        }
        distance[1] = 0
        while queue:
            dist, node = heapq.heappop(queue)
            for next_node in graph[node]:
                if distance[next_node] > dist:
                    distance[next_node] = dist
                    heapq.heappush(queue, (dist, next_node))
            for next_node in range(node + 1, min(node + 7, length + 1)):
                if distance[next_node] > dist + 1:
                    distance[next_node] = dist + 1
                    heapq.heappush(queue, (dist + 1, next_node))
        return distance[length]

    def build_graph(self, length, connections):
        graph = {
            i: set()
            for i in range(1, length + 1)
        }
        for a, b in connections:
            graph[a].add(b)
        return graph
```
