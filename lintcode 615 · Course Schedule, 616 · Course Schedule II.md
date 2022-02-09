## Example 1:

Input: n = 2, prerequisites = [[1,0]] 

Output: true

Example 2:

Input: n = 2, prerequisites = [[1,0],[0,1]] 

Output: false
```
class Solution:
    """
    @param numCourses: a total of n courses
    @param prerequisites: a list of prerequisite pairs
    @return: true if can finish all courses or false
    """
    def canFinish(self, numCourses, prerequisites):
        graph = [[] for i in range(numCourses)]
        in_degree = [0] * numCourses
        
        # 建图 record every in—depth for node
        for node_in, node_out in prerequisites:
            graph[node_out].append(node_in)
            in_degree[node_in] += 1
        
        num_choose = 0
        queue = collections.deque()
        
        # 将入度为 0 的编号加入队列
        for i in range(numCourses):
            if in_degree[i] == 0:
                queue.append(i)
        #取出队首的元素now，将其加入拓扑序列。
        while queue:
            now_pos = queue.popleft()
            num_choose += 1
            # 将每条邻边删去，如果入度降为 0，再加入队列
            for next_pos in graph[now_pos]:
                in_degree[next_pos] -= 1
                if in_degree[next_pos] == 0:
                    queue.append(next_pos)
        
        return num_choose == numCourses
```
## Example
Example 1:

Input: n = 2, prerequisites = [[1,0]] 

Output: [0,1]

Example 2:

Input: n = 4, prerequisites = [[1,0],[2,0],[3,1],[3,2]] 

Output: [0,1,2,3] or [0,2,1,3]

```
class Solution:
    """
    @param: numCourses: a total of n courses
    @param: prerequisites: a list of prerequisite pairs
    @return: the course order
    """
    def findOrder(self, numCourses, prerequisites):
        #构建图，代表（先修课->后修课）的映射
        #图的初始化，每个先修课-》后修课list
        graph = [[] for i in range(numCourses)]
        #1:统计每个点的入度，并构建图
        in_degree = [0] * numCourses
        for node_in, node_out in prerequisites:
            graph[node_out].append(node_in)
            in_degree[node_in] += 1
        #2:将每个入度为0的点，放入队列中作为起始点
        queue = collections.deque()
        for i in range(numCourses):
            if in_degree[i] == 0:
                queue.append(i)
        #记录已修改课程的数量
        num_choose = 0
        #记录拓扑顺序
        topo_order = []
        #3:不断从队列中拿出一个点，去掉这个点的所有连边（指向其他点的边）
        #其他点的对应入度 -1
        while queue:
            now_pos = queue.popleft()
            topo_order.append(now_pos)
            num_choose += 1
            #当前点的所有邻居入度-1， 表示每个后修课的一门先修课已完成
            for next_pos in graph[now_pos]:
                in_degree[next_pos] -= 1
                #4 一旦发现入度为0的点，丢回队列中
                #表示一门后修课的所有先修课已完成，可以开始修了
                if in_degree[next_pos] == 0:
                    queue.append(next_pos)
        #如果全部课程已经被修过，那么返回拓扑排序，否则为空
        return topo_order if num_choose == numCourses else []
```
