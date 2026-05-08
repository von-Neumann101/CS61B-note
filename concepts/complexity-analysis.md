---
type: concept
course: CS61B
priority: A
status: draft
aliases: []
related:
  - "[[array-list]]"
  - "[[binary-search-tree]]"
  - "[[hash-table]]"
  - "[[heap]]"
  - "[[union-find]]"
  - "[[graph]]"
---

# Complexity Analysis

## 一句话定义

[[complexity-analysis]] 是用输入规模增长时的操作次数或空间占用来评价算法和数据结构。它在 CS61B 中解决的问题是：不依赖某台机器的运行时间，而用增长阶比较实现策略。

## 核心思想

CS61B 关心的是规模变大后成本如何变化。实际运行时间受电脑、语言、常数因子影响；渐进分析把注意力放在最坏情况、增长阶和主导项上。比如单调数组查重时，逐对比较和只比较相邻项在小规模下都能跑，但增长后差异会被放大。

复杂度分析也服务工程选择。AList 的扩容策略、BST 的高度、hash table 的桶长、merge sort 的递归层数，都需要用复杂度语言表达。摊还分析说明“某一次很贵”不等于“长期很贵”；决策树下界说明比较排序必须通过足够多比较才能区分所有排列。

## 核心边界 / Contract / Invariant

无单一固定 invariant，重点在于抽象边界和使用约束。分析前必须说明输入规模是什么、统计什么操作、讨论 worst case 还是长期平均，以及忽略哪些常数和低阶项。

复杂度符号的 contract 是：[[3. DataStructure and Algorithm/渐进分析/L13 渐进分析2/L13 渐进分析2|big-o]] 表示上界，[[3. DataStructure and Algorithm/渐进分析/L13 渐进分析2/L13 渐进分析2|big-omega]] 表示下界，[[3. DataStructure and Algorithm/渐进分析/L11 渐进分析1/L11 渐进分析1|theta-notation]] 表示上下界同阶。若没有说明清楚问题模型，复杂度结论容易失真；例如比较排序下界不约束 radix sort 这类非比较排序。

## 在 CS61B 中的位置

[[complexity-analysis]] 是所有数据结构选择的共同语言。List 选择需要比较链表和数组，tree/hash/heap/union-find 需要解释操作成本，排序需要区分比较模型和非比较模型。它把实现细节、抽象接口和性能承诺连接起来。

## 典型实现

- 单调数组查重：解决如何比较算法好坏的问题；核心思想是用操作次数和最坏情况替代机器时间；相关概念：[[3. DataStructure and Algorithm/渐进分析/L11 渐进分析1/L11 渐进分析1|theta-notation]]。
- AList resizing：解决固定数组增长成本的问题；核心思想是比较加法扩容和乘法扩容的总复制次数；相关概念：[[array-list]]、[[3. DataStructure and Algorithm/渐进分析/L14 渐进分析3/L14 渐进分析3|amortized-analysis]]。
- Merge sort recurrence：解决递归排序成本问题；核心思想是每层处理 N 个元素，共 `lg N` 层；相关概念：[[3. DataStructure and Algorithm/渐进分析/L14 渐进分析3/L14 渐进分析3|recursion-tree]]、[[4. Sort/L30 Merge Sort, Insertion Sort, and Quick Sort/L30 Merge Sort, Insertion Sort, and Quick Sort|merge-sort]]。
- comparison sort lower bound：解决比较排序最优下界问题；核心思想是用决策树区分 `N!` 种排列；相关概念：[[4. Sort/L34 Sorting and Algorithmic Bounds/L34 Sorting and Algorithmic Bounds|decision-tree-lower-bound]]。

## 容易混淆点

- Big-O vs Theta：O 只给上界，Theta 表示同阶精确增长。
- worst case vs average behavior：BST 和 hash table 都可能因输入或分布退化。
- single operation cost vs amortized cost：扩容单次贵，但长期平均可能低。
- comparison sort vs non-comparison sort：决策树下界只约束基于比较的排序。
- recursion depth vs total work：递归层数不能直接等同总复杂度。

## 相关概念

- [[3. DataStructure and Algorithm/渐进分析/L13 渐进分析2/L13 渐进分析2|big-o]]
- [[3. DataStructure and Algorithm/渐进分析/L13 渐进分析2/L13 渐进分析2|big-omega]]
- [[3. DataStructure and Algorithm/渐进分析/L11 渐进分析1/L11 渐进分析1|theta-notation]]
- [[3. DataStructure and Algorithm/渐进分析/L14 渐进分析3/L14 渐进分析3|amortized-analysis]]
- [[3. DataStructure and Algorithm/渐进分析/L14 渐进分析3/L14 渐进分析3|recursion-tree]]
- [[4. Sort/L34 Sorting and Algorithmic Bounds/L34 Sorting and Algorithmic Bounds|decision-tree-lower-bound]]
- [[array-list]]

## 跨课程连接

- CS61A：连接递归过程的增长阶和 tree recursion。
- CSAPP：连接性能分析、常数因子和内存层级影响，但需要人工补充具体例子。
- Machine Learning：连接训练时间、数据规模和算法选择。
- UMich DL：连接模型训练计算量和 batch 规模，但需要人工补充具体例子。
