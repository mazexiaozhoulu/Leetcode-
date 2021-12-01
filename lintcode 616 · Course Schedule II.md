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
