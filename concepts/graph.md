---
type: concept
course: CS61B
priority: A
status: draft
aliases: []
related:
  - "[[tree]]"
  - "[[bfs]]"
  - "[[dfs]]"
  - "[[priority-queue]]"
  - "[[union-find]]"
  - "[[complexity-analysis]]"
---

# Graph

## 一句话定义

[[graph]] 是由 vertex 和 edge 组成的结构，用来表达任意节点之间的连接关系。它在 CS61B 中解决的问题是：统一表示路径、连通性、最短路、最小生成树和依赖顺序。

## 核心思想

图可以看作限制更少的树：允许环、允许反向连接，也不要求单一 root。正因为自由度更高，图算法必须显式维护 visited / marked，否则遍历可能重复访问或陷入环。

图的表示会直接影响算法复杂度。邻接矩阵查一条边方便，但输出所有边不合适；edge set 直接存边；邻接列表适合遍历邻居。L23 中强调，图数据结构应只提供原子功能，DFS、BFS、Dijkstra、MST 等算法放在独立逻辑中。

## 核心边界 / Contract / Invariant

核心 invariant 是：vertex 集合和 edge 集合必须一致，边只能连接存在的顶点；简单图不允许自环和平行边；邻接列表中每个顶点的列表表示它的邻居。对于无向图，一条边通常需要在两个方向的邻接关系中保持一致。

这个 invariant 保证遍历能枚举正确邻居，也让 `Theta(V + E)` 这类复杂度分析成立。如果邻接关系漏边、重复边或方向不一致，DFS/BFS 的可达性、路径恢复和 MST / shortest path 都可能出错。

## 在 CS61B 中的位置

[[graph]] 是 CS61B 后半段算法的统一模型。它承接 [[tree]] traversal，又连接 DFS、BFS、Dijkstra、Prim、Kruskal、topological sort。[[priority-queue]] 和 [[union-find]] 在这里变成算法组件，而不是孤立数据结构。

## 典型实现

- adjacency list graph：解决图遍历需要快速枚举邻居的问题；核心思想是每个 vertex 保存邻接顶点集合；相关概念：[[3. DataStructure and Algorithm/L23 BFS, DFS and implementations/L23 BFS, DFS and implementations|adjacency-list]]。
- DFS / BFS：解决可达性、路径和无权最短路径；核心思想是 DFS 沿路径深入，BFS 用 queue 逐层扩展；相关概念：[[3. DataStructure and Algorithm/L23 BFS, DFS and implementations/L23 BFS, DFS and implementations|bfs]]、[[3. DataStructure and Algorithm/L22 Tree and Graph Traversals/L22 Tree and Graph Traversals|dfs]]。
- Dijkstra：解决非负带权图最短路径；核心思想是用 priority queue 选择当前最短 distTo 顶点并松弛边；相关概念：[[priority-queue]]、[[3. DataStructure and Algorithm/L24 Shotest Path/L24 Shotest Path|dijkstra]]。
- MST: Prim / Kruskal：解决无向带权图的最小生成树；核心思想是 cut property，Prim 用 PQ，Kruskal 用 UnionFind 防环；相关概念：[[3. DataStructure and Algorithm/L25 Minimum Spinning Tree/L25 Minimum Spinning Tree|minimum-spanning-tree]]、[[union-find]]。
- DAG topological sort：解决有向无环依赖顺序；核心思想是 DFS 后序反转或按入度处理；相关概念：[[3. DataStructure and Algorithm/L26 Directed Acyclic Graphs/L26 Directed Acyclic Graphs|topological-sort]]。

## 容易混淆点

- tree vs graph：tree 有层级约束，graph 允许环和任意连接。
- adjacency matrix vs adjacency list：前者查边直接，后者遍历所有边和点更合适。
- DFS vs BFS：DFS 维护当前递归路径，BFS 用队列逐层扩展。
- BFS vs Dijkstra：BFS 默认边权相同，Dijkstra 处理非负权重。
- Prim vs Kruskal：Prim 从一个连通块扩展，Kruskal 按边权排序并用 UnionFind 防环。

## 相关概念

- [[tree]]
- [[priority-queue]]
- [[union-find]]
- [[3. DataStructure and Algorithm/L23 BFS, DFS and implementations/L23 BFS, DFS and implementations|bfs]]
- [[3. DataStructure and Algorithm/L22 Tree and Graph Traversals/L22 Tree and Graph Traversals|dfs]]
- [[3. DataStructure and Algorithm/L24 Shotest Path/L24 Shotest Path|dijkstra]]
- [[3. DataStructure and Algorithm/L25 Minimum Spinning Tree/L25 Minimum Spinning Tree|minimum-spanning-tree]]

## 跨课程连接

- CS61A：连接递归搜索和状态空间。
- CSAPP：控制流图、依赖图可作弱连接，需要人工补充。
- Machine Learning：连接图模型、搜索和传播。
- UMich DL：连接 computation graph。
