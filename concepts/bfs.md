---
type: concept
course: CS61B
priority: A
status: draft
aliases: []
related:
  - "[[graph]]"
  - "[[dfs]]"
  - "[[priority-queue]]"
  - "[[complexity-analysis]]"
---

# Breadth-First Search

## 一句话定义

[[bfs]] 是从起点开始按层扩展访问图或树的遍历算法。它在 CS61B 中解决的问题是：在无权图中找到从 source 到其他顶点的最短步数路径。

## 核心思想

BFS 用 queue 保存 fringe，也就是下一批要访问的边缘顶点。起点距离为 0，每弹出一个顶点，就把未访问邻居加入队列，并把它们的距离设为当前距离加 1。因为 queue 保证先发现的层先处理，所以第一次到达某个顶点时，路径边数就是最短的。

这也说明了 BFS 的边界：它把每条边都看作同样代价。L24 明确指出，有权图中 BFS 会默认所有权重相等，因此不能处理一般 weighted shortest path；非负带权图需要 Dijkstra，用 priority queue 按当前距离选择顶点。

## 核心边界 / Contract / Invariant

核心 invariant 是：queue 中的顶点按距离层次从小到大等待处理；`visited` / marked 防止重复入队；`distTo` 记录从 source 到顶点的层数；`edgeTo` 记录路径来自哪个前驱。

这个 invariant 保证 BFS 第一次访问某顶点时得到的是无权最短路径。如果不维护 visited，图中有环时可能重复访问或无限扩展；如果 queue 被换成 stack，就会变成 DFS，不再保证无权最短路径。

## 在 CS61B 中的位置

[[bfs]] 是 [[graph]] traversal 的核心算法之一，接在 tree level-order traversal 之后。它和 [[dfs]] 共同构成图搜索基础，并向后连接 shortest path：无权图用 BFS，非负带权图用 [[3. DataStructure and Algorithm/L24 Shotest Path/L24 Shotest Path|dijkstra]]。

## 典型实现

- Graph BFS：解决从 source 到所有可达顶点的层次搜索；核心思想是 queue、visited、distTo；相关概念：[[graph]]、[[3. DataStructure and Algorithm/L23 BFS, DFS and implementations/L23 BFS, DFS and implementations|fringe]]。
- path recovery with edgeTo：解决输出实际路径的问题；核心思想是为每个顶点记录它从哪个顶点被发现；相关概念：[[3. DataStructure and Algorithm/L23 BFS, DFS and implementations/L23 BFS, DFS and implementations|edgeTo]]。
- unweighted shortest path：解决无权图最短边数路径；核心思想是每一层 dist 加 1；相关概念：[[3. DataStructure and Algorithm/L24 Shotest Path/L24 Shotest Path|shortest-path]]。
- Dijkstra contrast：解决 BFS 不能处理 weighted graph 的问题；核心思想是改用 priority queue 和 relaxation；相关概念：[[priority-queue]]、[[3. DataStructure and Algorithm/L24 Shotest Path/L24 Shotest Path|dijkstra]]。

## 容易混淆点

- BFS vs DFS：BFS 用 queue 逐层扩展，DFS 沿路径深入。
- BFS shortest path vs Dijkstra：BFS 只适合无权或等权图，Dijkstra 处理非负权重。
- visited vs edgeTo：visited 防止重复访问，edgeTo 用于恢复路径。
- queue fringe vs recursion stack：BFS 的 fringe 是队列，DFS 的递归栈只保存当前路径。
- time vs space：BFS 时间可随邻接列表遍历达到 `Theta(V + E)`，空间受最大层宽影响。

## 相关概念

- [[graph]]
- [[dfs]]
- [[priority-queue]]
- [[3. DataStructure and Algorithm/L23 BFS, DFS and implementations/L23 BFS, DFS and implementations|graph-traversal]]
- [[3. DataStructure and Algorithm/L24 Shotest Path/L24 Shotest Path|shortest-path]]
- [[3. DataStructure and Algorithm/L24 Shotest Path/L24 Shotest Path|dijkstra]]

## 跨课程连接

- CS61A：连接树/图搜索和层序遍历。
- CSAPP：状态空间搜索有弱连接，需要人工补充。
- Machine Learning：连接图传播、搜索和最短步数问题。
- UMich DL：图或 computation graph 的层级遍历有弱连接，需要人工补充。
