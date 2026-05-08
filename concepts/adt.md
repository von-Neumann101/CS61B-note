---
type: concept
course: CS61B
priority: A
status: draft
aliases: []
related:
  - "[[abstraction]]"
  - "[[interface]]"
  - "[[linked-list]]"
  - "[[array-list]]"
  - "[[hash-table]]"
  - "[[priority-queue]]"
---

# Abstract Data Type

## 一句话定义

[[adt|ADT]] 是用一组操作和行为契约描述数据类型，而不是描述它在内存里怎么存。它在 CS61B 中解决的问题是：客户端应依赖 `add`、`get`、`contains`、`remove` 这类稳定操作，而不是依赖节点、数组、桶或树节点。

## 核心思想

ADT 先问“这个类型承诺能做什么”，再让实现类决定“怎么做到”。同一个 List ADT 可以由 [[1. Introduction to Java/L4 SLList/L4 SLList|sllist]] 或 [[array-list]] 实现，同一个 Set / Map 思想可以由 BST 或 hash table 支撑。这样客户端代码可以面向抽象写，具体类再根据复杂度、内存布局和 invariant 做工程选择。

ADT 的价值不是让实现消失，而是把实现的变化限制在抽象边界内。只要操作契约不变，底层从链表换成数组、从 BST 换成 hash table，都不应该迫使客户端重写逻辑。

## 核心边界 / Contract / Invariant

client 能依赖的是公开方法的语义、参数和返回结果，例如 List 的插入、读取、长度查询，Set 的 membership，Map 的 key-value 查询。implementation 隐藏的是内部表示：`IntNode`、底层数组、bucket、树节点、邻接表。

ADT 的 contract 是：每个公开操作必须保持数据类型对外可观察行为一致。无单一固定 invariant，重点在于抽象边界和使用约束；具体 invariant 属于实现类，例如 SLList 的 `first`、AList 的 size/capacity、BST 的 ordered property。

## 在 CS61B 中的位置

[[abstraction]] 给出设计原则，[[adt|ADT]] 把原则落到“操作集合”，[[interface]] 再用 Java 类型系统表达这些操作。CS61B 后续的 List、Set、Map、PriorityQueue、Graph 都是先作为 ADT 理解，再比较不同实现的复杂度和维护成本。

## 典型实现

- List61B：解决不同 List 实现复用客户端代码的问题；核心思想是把列表操作放进统一接口；相关概念：[[interface]]、[[linked-list]]、[[array-list]]。
- SLList / AList：解决同一 List ADT 的不同存储策略；核心思想是链式节点 vs 连续数组；相关概念：[[1. Introduction to Java/L4 SLList/L4 SLList|sllist]]、[[3. DataStructure and Algorithm/渐进分析/L14 渐进分析3/L14 渐进分析3|resizing-array]]。
- HashSet / BST Map：解决 membership 或 key 查询；核心思想是用 hash 或 ordered invariant 支撑操作；相关概念：[[hash-table]]、[[binary-search-tree]]。
- PriorityQueue / Graph：作为后续算法依赖的抽象操作集合；实现细节需要人工补充。

## 容易混淆点

- [[ADT]] vs concrete class：ADT 是行为契约，class 是一种实现。
- [[abstraction]] vs [[ADT]]：abstraction 是设计原则，ADT 是表达数据类型的方式。
- [[interface]] vs [[ADT]]：interface 是 Java 机制，ADT 是语言无关的概念。
- operation contract vs implementation detail：方法语义可以依赖，内部表示不应该依赖。

## 相关概念

- [[abstraction]]
- [[interface]]
- implementation
- invariant
- [[linked-list]]
- [[array-list]]

## 跨课程连接

- CS61A：连接 data abstraction、pair/list/tree 这类用操作隐藏表示的思想。
- CSAPP：连接接口与实现分层，但需要人工补充更具体系统例子。
- Machine Learning：Dataset / Model / Optimizer 可看作操作契约，具体训练细节隐藏在实现后。
- UMich DL：layer、module、loss function 都依赖稳定接口和可替换实现。
