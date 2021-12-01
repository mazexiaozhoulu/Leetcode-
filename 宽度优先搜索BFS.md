适用场景：

分层遍历：一层一层的遍历一个图、树、矩阵； 简单图的最短路径

连通块问题：通过途中提个点找到其他所有连通的点；找到所欲方案问题的一种非递归实现方式

拓扑排序：实现容易度远超DFS

BFS:
[69](https://github.com/mazexiaozhoulu/Leetcode-/blob/ae8412a44d6b63113da89660090c338aef31a4ee/lintcode%2069%20%C2%B7%20Binary%20Tree%20Level%20Order%20Traversal.md)

BFS（包括图）：N个点 M条边 图上BFS时间复杂度=O(n+m)
[137](https://github.com/mazexiaozhoulu/Leetcode-/blob/312a5248f9c2cbf6b1a0a74c7a784f4f2971f164/lintcode%20137%20Clone%20Graph.md)
[120](https://github.com/mazexiaozhoulu/Leetcode-/blob/b630373864d717297c04845fbfafd30649c5210b/lintcode%20120%20%C2%B7%20Word%20Ladder.md)
[433](https://github.com/mazexiaozhoulu/Leetcode-/blob/d3f6f1bdd35c8ce1c3afaa522a73d17433bde9f2/lintcode%20433%20%C2%B7%20Number%20of%20Islands.md)
[611](https://github.com/mazexiaozhoulu/Leetcode-/blob/b00f383aa97ffadada1e7e48677842a2fa47931e/lintcode%20611%20%C2%B7%20Knight%20Shortest%20Path.md)
```
queue = collections.deque([node])
distance = {node:0}

while queue:
  node = queue.popleft()
  for neighbor in node.get_neighbors():
    if neighbor in distance:
      continue
    distance[neighbor] = distance[node] +1
    queue.append(neighbor)
```

#拓扑排序：

[616](https://github.com/mazexiaozhoulu/Leetcode-/blob/0d998842787bac33cc717d3ef6b26c2ac7d2001b/lintcode%20616%20%C2%B7%20Course%20Schedule%20II.md)
图+有依赖关系+有向+无环

入度（in depth)；有向图中指向当前节点的点的个数

算法描述：
>统计每个点的入度

>将每个入度为0的点，放入队列中作为起始节点

>不断地从队列中拿出一个点，去掉这个点的所有连边，其他点的相应入度 -1

>一旦发现入度为0的点，丢回队列
