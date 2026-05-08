---
type: concept
course: CS61B
priority: A
status: draft
aliases: []
related:
  - "[[tree]]"
  - "[[priority-queue]]"
  - "[[array-list]]"
  - "[[complexity-analysis]]"
---

# Heap

## 一句话定义

[[heap]] 是满足 complete tree 形状约束和 heap property 的树形数据结构。它在 CS61B 中解决的问题是：不维护全局排序，也能快速得到最小或最大元素。

## 核心思想

heap 的关键是弱 invariant。以 binary min-heap 为例，只要求每个节点小于等于自己的子节点，不要求左子树所有元素都小于右子树，也不支持像 BST 那样按 key 搜索。这个弱约束足够保证 root 是最小值，因此 `getSmallest` 可以直接看 root。

complete tree 让 heap 很适合用数组实现。因为每层尽量填满，且最底层从左到右填，父子关系可以由下标推导出来，不需要显式 parent 指针。`add` 把新元素放到最后再向上交换，`removeSmallest` 把最后元素放到 root 再向下交换。

## 核心边界 / Contract / Invariant

核心 invariant 是：树必须是 complete binary tree；min-heap 中每个节点的 label 小于等于其子节点 label。数组实现还依赖“节点按层序紧密存放”，这样 parent/child index 才有意义。

这个 invariant 保证 root 一定是最小元素，`swim` 和 `sink` 只需沿一条父子路径修复局部错误。如果 heap property 被破坏，`getSmallest` 可能返回错误元素；如果 complete property 被破坏，数组下标和树结构会失配。

## 在 CS61B 中的位置

[[heap]] 接在 [[tree]] 之后，但和 [[binary-search-tree]] 走不同路线：BST 用较强有序 invariant 支持搜索，heap 用较弱局部 invariant 支持极值访问。它是 [[priority-queue]]、heap sort、Dijkstra 和 Prim 的基础实现工具。

## 典型实现

- Binary min-heap：解决快速获取最小元素的问题；核心思想是 root 最小，add swim，removeSmallest sink；相关概念：[[3. DataStructure and Algorithm/L21 Priority queue, Heap/L21 Priority queue, Heap|heap-property]]、[[priority-queue]]。
- array-backed heap：解决树节点指针开销和 parent 查找问题；核心思想是利用 complete tree 的层序布局推导父子下标；相关概念：[[array-list]]、[[3. DataStructure and Algorithm/L21 Priority queue, Heap/L21 Priority queue, Heap|complete-tree]]。
- heap sort：解决选择排序每次找极值太慢的问题；核心思想是用 heap 反复取出最大或最小元素；相关概念：[[4. Sort/L28 Sorting1/L28 Sorting1|heap-sort]]、[[complexity-analysis]]。

## 容易混淆点

- heap vs priority queue：heap 是实现结构，priority queue 是 ADT。
- heap invariant vs BST invariant：heap 只约束父子，BST 约束整棵左右子树。
- complete tree vs balanced tree：complete 是形状填充规则，不等于一般平衡树。
- getSmallest vs search：heap 能快速看最小值，但不能高效查找任意 key。
- swim vs sink：add 后向上修复，remove root 后向下修复。

## 相关概念

- [[tree]]
- [[priority-queue]]
- [[array-list]]
- [[complexity-analysis]]
- [[4. Sort/L28 Sorting1/L28 Sorting1|heap-sort]]

## 跨课程连接

- CS61A：连接树结构和递归层级思想。
- CSAPP：连接数组布局和隐式结构表示。
- Machine Learning：top-k、beam search 可用优先级思想连接，但需要人工补充具体例子。
- UMich DL：top-k / priority scheduling 有弱连接，需要人工补充。
