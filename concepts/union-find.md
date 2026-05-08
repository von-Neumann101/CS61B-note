---
type: concept
course: CS61B
priority: A
status: draft
aliases: []
related:
  - "[[tree]]"
  - "[[graph]]"
  - "[[complexity-analysis]]"
---

# Union Find

## 一句话定义

[[union-find]] 是维护若干不相交集合的数据结构，核心操作是 `connect` / `union` 和 `isConnected`。它在 CS61B 中解决的问题是：动态合并集合，并快速判断两个元素是否属于同一连通分量。

## 核心思想

UnionFind 最终用树表示每个集合。`isConnected(x, y)` 判断两个元素是否有相同 root；`connect(x, y)` 把两个集合的 root 连起来。连接方式决定性能，如果随便连接，树可能退化成链表。

weighted quick union 的思想是让小树接到大树下面，控制树高。path compression 则在查 root 的过程中，把路径上的节点顺手直接连到 root。前者限制坏形状增长，后者让后续查询更快，是 CS61B 中“维护 invariant + 摊还优化”的典型例子。

## 核心边界 / Contract / Invariant

核心 invariant 是：每个集合是一棵以 root 表示代表元的树；同一集合内所有节点最终能追溯到同一个 root；union 时必须根连根，否则可能丢失已有子树结构。weighted 版本还维护每棵树的 size，用于决定小树接大树。

这个 invariant 保证 `isConnected` 可以只比较 root。如果 parent 指针形成错误结构、非 root 被直接接错，或 size 信息不同步，可能导致连通性判断错误，或者让树退化到接近线性高度。

## 在 CS61B 中的位置

[[union-find]] 是图算法前的重要结构。它把 [[tree]] 的表示用于动态连通性，并在 Kruskal MST 中用于检测加入一条边是否会成环。它也连接 [[complexity-analysis]]，因为 weighted union 和 path compression 的组合接近常数时间。

## 典型实现

- QuickFind：解决快速判断集合编号是否相同的问题；核心思想是同一集合共享 id；笔记只简略讨论，细节需要人工补充。
- Weighted Quick Union：解决随意连接导致树太高的问题；核心思想是根连根，小树接大树；相关概念：[[3. DataStructure and Algorithm/L15 Disjoint Set/L15 Disjoint Set|weighted-quick-union]]。
- Path Compression：解决重复查 root 路径过长的问题；核心思想是查询时把沿途节点直接接到 root；相关概念：[[3. DataStructure and Algorithm/L15 Disjoint Set/L15 Disjoint Set|path-compression]]。
- Kruskal cycle detection：解决 MST 加边时判断是否成环的问题；核心思想是若边两端已 connected，则加入会成环；相关概念：[[3. DataStructure and Algorithm/L25 Minimum Spinning Tree/L25 Minimum Spinning Tree|kruskal-algorithm]]、[[graph]]。

## 容易混淆点

- union/connect vs isConnected：前者改变集合，后者只查询关系。
- root vs parent：root 是集合代表，parent 只是通向 root 的一步。
- weighted union vs path compression：前者控制合并方向，后者优化查询路径。
- graph connectivity vs UnionFind structure：UnionFind 不存完整图，只维护连通分量关系。
- Kruskal vs Prim：Kruskal 用 UnionFind 防环，Prim 用 priority queue 扩展 cut。

## 相关概念

- [[tree]]
- [[graph]]
- [[complexity-analysis]]
- [[3. DataStructure and Algorithm/L15 Disjoint Set/L15 Disjoint Set|disjoint-set]]
- [[3. DataStructure and Algorithm/L25 Minimum Spinning Tree/L25 Minimum Spinning Tree|kruskal-algorithm]]

## 跨课程连接

- CS61A：连接集合抽象。
- CSAPP：连接较弱，需要人工补充。
- Machine Learning：聚类连通分量有弱连接，需要人工补充。
- UMich DL：连接较弱，需要人工补充。
