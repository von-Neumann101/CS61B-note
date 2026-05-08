---
type: concept-map
course: CS61B
priority: A
status: draft
aliases:
  - CS61B concept graph
  - CS61B knowledge graph
related:
  - "[[abstraction]]"
  - "[[adt]]"
  - "[[interface]]"
  - "[[complexity-analysis]]"
  - "[[tree]]"
  - "[[graph]]"
---

# CS61B Concept Graph

## 主干路径

[[abstraction]] -> [[adt]] -> [[interface]] -> [[polymorphism]] -> [[generics]]

[[adt]] -> [[linked-list]] -> [[array-list]] -> [[complexity-analysis]]

[[tree]] -> [[binary-search-tree]] -> [[hash-table]]

[[tree]] -> [[heap]] -> [[priority-queue]] -> [[graph]]

[[graph]] -> [[bfs]] / [[dfs]]

[[tree]] -> [[union-find]] -> [[graph]]

## 抽象与类型

- [[abstraction]]：把 client contract 和 implementation detail 分开。
- [[adt]]：用操作集合描述数据类型行为。
- [[interface]]：用 Java 类型系统表达可依赖的行为边界。
- [[polymorphism]]：让同一 client 代码通过共同类型处理不同实现。
- [[generics]]：让容器和算法在多种元素类型上保持类型安全。

## 线性结构与复杂度

- [[linked-list]]：用节点引用表示可增长线性序列。
- [[array-list]]：用底层数组表示可增长逻辑列表。
- [[complexity-analysis]]：比较不同实现随输入规模增长的成本。
- [[hash-table]]：继承 array-backed resizing 的直觉，用 bucket 支撑 set/map 查询。

## 树与有序结构

- [[tree]]：从线性引用结构扩展到递归分支结构。
- [[binary-search-tree]]：用 ordered invariant 支撑查找、插入、删除。
- [[heap]]：用 complete tree 和 heap property 支撑极值访问。
- [[union-find]]：用 forest 表示 disjoint sets 和动态连通性。

## 图与算法组件

- [[graph]]：统一表示路径、连通性、最短路、MST 和依赖顺序。
- [[bfs]]：按层扩展，支撑无权图最短路径。
- [[dfs]]：沿路径深入，支撑可达性、路径恢复和拓扑顺序。
- [[priority-queue]]：在 Dijkstra、Prim 等算法中管理当前最优候选。
- [[union-find]]：在 Kruskal 等算法中检测连通性和成环。

## 邻接表

- [[abstraction]] -> [[adt]], [[interface]], [[linked-list]], [[array-list]], [[hash-table]], [[graph]]
- [[adt]] -> [[abstraction]], [[interface]], [[linked-list]], [[array-list]], [[hash-table]], [[priority-queue]]
- [[interface]] -> [[abstraction]], [[adt]], [[polymorphism]], [[generics]], [[linked-list]], [[array-list]]
- [[polymorphism]] -> [[interface]], [[generics]], [[adt]], [[abstraction]]
- [[generics]] -> [[interface]], [[polymorphism]], [[adt]], [[binary-search-tree]], [[priority-queue]]
- [[linked-list]] -> [[abstraction]], [[adt]], [[array-list]], [[tree]], [[complexity-analysis]]
- [[array-list]] -> [[adt]], [[linked-list]], [[complexity-analysis]], [[hash-table]], [[heap]]
- [[complexity-analysis]] -> [[array-list]], [[binary-search-tree]], [[hash-table]], [[heap]], [[union-find]], [[graph]]
- [[tree]] -> [[linked-list]], [[binary-search-tree]], [[heap]], [[union-find]], [[graph]], [[dfs]]
- [[binary-search-tree]] -> [[tree]], [[complexity-analysis]], [[hash-table]], [[generics]]
- [[hash-table]] -> [[adt]], [[array-list]], [[complexity-analysis]], [[binary-search-tree]], [[graph]]
- [[heap]] -> [[tree]], [[priority-queue]], [[array-list]], [[complexity-analysis]]
- [[priority-queue]] -> [[heap]], [[graph]], [[complexity-analysis]], [[bfs]]
- [[union-find]] -> [[tree]], [[graph]], [[complexity-analysis]]
- [[graph]] -> [[tree]], [[bfs]], [[dfs]], [[priority-queue]], [[union-find]], [[complexity-analysis]]
- [[bfs]] -> [[graph]], [[dfs]], [[priority-queue]], [[complexity-analysis]]
- [[dfs]] -> [[graph]], [[tree]], [[bfs]]
