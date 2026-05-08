---
type: concept
course: CS61B
priority: A
status: draft
aliases:
  - abstraction
related:
  - "[[adt]]"
  - "[[interface]]"
  - "[[linked-list]]"
  - "[[array-list]]"
  - "[[hash-table]]"
  - "[[graph]]"
---

# Abstraction

## 一句话定义

[[abstraction]] 是把 client 需要依赖的操作和 implementation 内部如何存储、维护分开。它在 CS61B 中解决的问题是：客户端代码应该依赖稳定接口，而不是依赖节点、数组、桶、树节点或邻接表等内部表示。

## 核心思想

Abstraction 的重点不是“不看实现”，而是先划清使用边界。Client 只通过公开方法使用数据结构；implementation 负责选择表示、维护 invariant，并在不破坏外部 contract 的前提下优化性能。

这条线贯穿 CS61B：从裸露节点到 `SLList`，再到 `AList`、hash table、priority queue、graph。每次引入新结构，课程都在问同一个问题：哪些行为应暴露给使用者，哪些细节必须被封装起来。

## 核心边界 / Contract / Invariant

无单一固定 invariant，重点在于抽象边界和使用约束。

- Client 能依赖公开操作的行为和复杂度承诺，不能依赖内部字段或节点布局。
- Implementation 隐藏底层表示，例如 linked nodes、array resizing、bucket、heap array、adjacency list。
- Contract 是“方法在什么输入下返回什么结果、是否修改结构、复杂度大致如何”。
- Invariant 由实现维护；如果 client 能绕过抽象屏障直接改内部状态，数据结构可能失去正确性。

## 在 CS61B 中的位置

[[abstraction]] 是 CS61B 数据结构主线的起点：[[abstraction]] -> [[adt]] -> [[interface]] -> implementation。后续的 [[linked-list]]、[[array-list]]、[[hash-table]]、[[heap]]、[[graph]] 都是在同一个 ADT 或算法目标下比较不同实现边界和复杂度。

## 典型实现

- `SLList`：解决裸节点暴露导致 client 可破坏链表的问题；核心思想是用列表类封装节点引用；相关概念：[[linked-list]]、[[adt]]。
- `AList`：解决同一 List ADT 的数组表示问题；核心思想是隐藏 resizing 和底层容量；相关概念：[[array-list]]、[[complexity-analysis]]。
- Hash table：解决 set/map 快速查询但隐藏 bucket 和 collision 细节；核心思想是对外提供 membership 或 key lookup；相关概念：[[hash-table]]。
- Graph adjacency list：解决图表示和图算法分离；核心思想是图结构提供邻居关系，算法如 [[bfs]] / [[dfs]] 在其上运行；相关概念：[[graph]]。

## 容易混淆点

- abstraction vs ignorance：抽象不是不理解实现；实现者仍必须维护 invariant 和复杂度。
- [[adt]] vs concrete class：ADT 说明行为契约，class 是一种具体实现。
- [[interface]] vs implementation：interface 说明能做什么，implementation 决定怎么做。
- hidden representation vs hidden cost：隐藏表示不等于隐藏复杂度，CS61B 仍要求比较操作成本。

## 相关概念

- [[adt]]
- [[interface]]
- [[linked-list]]
- [[array-list]]
- [[hash-table]]
- [[graph]]

## 跨课程连接

- CS61A：连接数据抽象、递归 list / tree 和抽象屏障。
- CSAPP：连接内存表示、指针结构和系统接口对机器细节的隐藏。
- Machine Learning：连接模型接口、数据表示和训练流程分离。
- UMich DL：连接 layer / module 抽象和张量操作封装。
