---
type: concept
course: CS61B
priority: A
status: draft
aliases: []
related:
  - "[[adt]]"
  - "[[linked-list]]"
  - "[[complexity-analysis]]"
  - "[[hash-table]]"
  - "[[heap]]"
---

# Array List

## 一句话定义

[[array-list]] 是用底层数组实现逻辑上可增长的 List。它在 CS61B 中解决的问题是：相比 [[linked-list]] 需要沿节点遍历，数组表示可以让按 index 访问更直接，但必须处理固定长度和 resizing。

## 核心思想

数组本身长度固定，ArrayList 的关键是把“逻辑长度”和“物理容量”分开。client 看到的是一个会增长的 List；implementation 维护一个数组、一个 size，并在容量不够时创建更大的数组，把旧元素复制过去。

这张卡的重点不是 Java 标准库的完整 API，而是 AList 这个工程案例：底层表示可以换成数组，但抽象边界不变。扩容策略直接影响长期成本；每次加常数容量会让总复制成本退化到平方级，而乘法扩容能把连续添加的总成本控制在线性量级，从而得到摊还意义上的高效 add。

## 核心边界 / Contract / Invariant

核心 invariant 是：`size` 表示当前有效元素数量，底层数组的前 `size` 个位置保存 List 内容，`size` 之后的位置只是备用容量；数组容量必须至少能容纳当前 size。对 client 来说，底层数组长度、复制时机和空槽都不属于可依赖行为。

这个 invariant 保证 `get(i)` 能在有效范围内直接定位元素，也保证 add 时知道应写入哪个位置。如果 `size` 和实际元素不同步，可能读到空槽、覆盖元素，或在还没扩容时越界。

## 在 CS61B 中的位置

[[array-list]] 接在 [[linked-list]] 之后，用同一个 List ADT 展示另一种表示选择。它连接数组、抽象屏障、[[3. DataStructure and Algorithm/渐进分析/L14 渐进分析3/L14 渐进分析3|resizing-array]] 和 [[3. DataStructure and Algorithm/渐进分析/L14 渐进分析3/L14 渐进分析3|amortized-analysis]]，也是后续 hash table resizing、heap 的 array-backed 表示的前置直觉。

## 典型实现

- AList：解决链表按 index 访问慢的问题；核心思想是用数组保存连续元素，并隐藏底层数组；相关概念：[[adt|ADT]]、[[1. Introduction to Java/L4 SLList/L4 SLList|abstraction-barrier]]。
- resizing array：解决数组固定长度的问题；核心思想是容量不够时分配更大数组并复制；相关概念：[[3. DataStructure and Algorithm/渐进分析/L14 渐进分析3/L14 渐进分析3|resizing-array]]、[[3. DataStructure and Algorithm/渐进分析/L14 渐进分析3/L14 渐进分析3|amortized-analysis]]。
- `System.arraycopy`：解决数组复制成本和实现细节问题；核心思想是把一段数组复制到另一段；相关概念：[[1. Introduction to Java/L5 List/L5 List|array]]。
- Hash table bucket array：解决桶数量需要随元素增长调整的问题；核心思想与数组扩容相通；相关概念：[[hash-table]]、[[3. DataStructure and Algorithm/L19 Hashing I/L19 Hashing I|resizing]]。

## 容易混淆点

- logical size vs array capacity：size 是元素数，capacity 是数组可容纳空间。
- array-list vs linked-list：前者依赖连续数组和扩容，后者依赖节点引用。
- resizing cost vs amortized cost：单次扩容很贵，但乘法扩容下长期平均成本可控。
- exposing array vs List abstraction：client 不应依赖内部数组长度或空槽。
- constant growth vs multiplicative growth：前者会导致总复制成本过高，后者减少扩容次数。

## 相关概念

- [[linked-list]]
- [[3. DataStructure and Algorithm/渐进分析/L14 渐进分析3/L14 渐进分析3|resizing-array]]
- [[3. DataStructure and Algorithm/渐进分析/L14 渐进分析3/L14 渐进分析3|amortized-analysis]]
- [[1. Introduction to Java/L4 SLList/L4 SLList|abstraction-barrier]]
- [[adt|ADT]]
- [[hash-table]]

## 跨课程连接

- CS61A：连接 sequence abstraction，但底层数组实现不是 CS61A 重点。
- CSAPP：连接连续内存、数组布局和复制成本。
- Machine Learning：连接数组化数据和 batch storage，但需要人工补充具体例子。
- UMich DL：可远连接 tensor storage，但当前 CS61B 笔记没有充分依据，需要人工补充。
