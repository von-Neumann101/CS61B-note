---
type: concept
course: CS61B
priority: A
status: draft
aliases: []
related:
  - "[[graph]]"
  - "[[tree]]"
  - "[[bfs]]"
---

# Depth-First Search

## 一句话定义

[[dfs]] 是沿一条路径尽量深入，走不通再回溯的图或树遍历算法。它在 CS61B 中解决的问题是：判断可达性、恢复路径，并支撑前序/后序、拓扑排序等结构性处理。

## 核心思想

DFS 的核心是递归路径。L22 笔记中强调，DFS stack 只保存当前递归路径；回溯时调用返回，路径上的节点自然弹出。对 tree 来说，前序、后序都是 DFS 的不同访问时机；对 graph 来说，必须用 marked / visited 防止环导致重复访问。

DFS 不保证无权最短路径，但它很适合探索结构。`edgeTo` 可以记录路径来源，preorder/postorder 可以表达“进入节点前做事”或“子问题完成后做事”。DAG 的拓扑排序也依赖 DFS 后序反转，让每条边都指向排序后方。

## 核心边界 / Contract / Invariant

核心 invariant 是：marked 记录已经访问过的顶点；递归栈表示当前探索路径；`edgeTo[w] = v` 表示 w 是从 v 被发现的。对于拓扑排序，还依赖图是 DAG，否则不存在全局依赖顺序。

这个 invariant 保证 DFS 不会在有环图中无限递归，并能在搜索成功后沿 edgeTo 还原路径。如果不维护 marked，图遍历会重复访问；如果把 DFS 用作最短路径算法，可能得到可达路径但不是最短路径。

## 在 CS61B 中的位置

[[dfs]] 从 [[tree]] traversal 延伸到 [[graph]] traversal。它和 [[bfs]] 共同构成图搜索基础：DFS 强在可达性、路径、前序/后序和 DAG 拓扑排序；BFS 强在无权最短路径。

## 典型实现

- recursive graph DFS：解决可达性搜索；核心思想是访问顶点、标记顶点、递归访问未标记邻居；相关概念：[[graph]]、[[3. DataStructure and Algorithm/L22 Tree and Graph Traversals/L22 Tree and Graph Traversals|marked]]。
- path recovery with edgeTo：解决搜索后输出路径；核心思想是记录每个顶点由哪个前驱发现；相关概念：[[3. DataStructure and Algorithm/L22 Tree and Graph Traversals/L22 Tree and Graph Traversals|edgeTo]]。
- preorder / postorder traversal：解决不同访问时机的问题；核心思想是操作放在递归前或递归后；相关概念：[[tree]]、[[3. DataStructure and Algorithm/L22 Tree and Graph Traversals/L22 Tree and Graph Traversals|tree-traversal]]。
- topological sort：解决 DAG 中依赖顺序；核心思想是 DFS 后序反转；相关概念：[[3. DataStructure and Algorithm/L26 Directed Acyclic Graphs/L26 Directed Acyclic Graphs|topological-sort]]、[[graph]]。

## 容易混淆点

- DFS vs BFS：DFS 深入当前路径，BFS 按层扩展。
- DFS path vs shortest path：DFS 能找到一条路径，但通常不保证最短。
- tree traversal vs graph traversal：tree 默认无环，graph 必须 marked。
- preorder vs postorder：前序先处理当前节点，后序先处理子结构。
- topological sort vs arbitrary DFS order：拓扑排序要求 DAG，并使用后序反转等规则。

## 相关概念

- [[graph]]
- [[tree]]
- [[bfs]]
- [[3. DataStructure and Algorithm/L22 Tree and Graph Traversals/L22 Tree and Graph Traversals|graph-traversal]]
- [[3. DataStructure and Algorithm/L26 Directed Acyclic Graphs/L26 Directed Acyclic Graphs|topological-sort]]

## 跨课程连接

- CS61A：连接 tree recursion、recursive search。
- CSAPP：递归栈和状态探索有弱连接，需要人工补充。
- Machine Learning：图搜索和依赖遍历有弱连接，需要人工补充。
- UMich DL：computation graph traversal 有弱连接，需要人工补充。
