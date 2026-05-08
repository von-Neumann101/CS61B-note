---
type: concept
course: CS61B
priority: A
status: draft
aliases: []
related:
  - "[[heap]]"
  - "[[graph]]"
  - "[[complexity-analysis]]"
  - "[[bfs]]"
---

# Priority Queue

## 一句话定义

[[priority-queue]] 是按优先级取元素的 ADT，典型 MinPQ 支持 `add`、`getSmallest`、`removeSmallest` 和 `size`。它在 CS61B 中解决的问题是：当算法每一步都需要当前最小候选时，不必反复线性扫描。

## 核心思想

priority queue 的抽象重点是操作语义，而不是底层结构。L21 的高能粒子例子中，只需要保留前 M 个最大值：元素超过 M 后立刻移除最小值，就能用固定规模结构处理大量输入。

在图算法中，priority queue 保存“当前最有希望的候选”。Dijkstra 根据当前最短 `distTo` 弹出顶点，Prim 根据当前 crossing edge 的权重选择边。这里常需要 `decreasePriority`：当发现更小距离或更小边权时，更新已有候选的优先级。

## 核心边界 / Contract / Invariant

client 能依赖的是：`getSmallest` 返回当前最小优先级元素，`removeSmallest` 删除并返回它，`add` 插入新元素，`size` 反映元素数量。implementation 隐藏排序数组、BST、heap 等具体策略。

PriorityQueue 本身无单一固定 invariant，重点在于抽象边界和使用约束；如果用 [[heap]] 实现，则核心 invariant 是 complete tree 与 heap property。如果实现不能保持最小元素可被正确取出，Dijkstra、Prim 这类算法会直接失去正确性。

## 在 CS61B 中的位置

[[priority-queue]] 位于数据结构和图算法之间。[[heap]] 给它高效实现，[[graph]] 算法把它用作候选集合，[[complexity-analysis]] 则解释为什么比数组扫描更适合反复取最小的场景。

## 典型实现

- Binary heap MinPQ：解决 `add` 和 `removeSmallest` 都需要高效的问题；核心思想是用 heap property 保证 root 最小；相关概念：[[heap]]、[[3. DataStructure and Algorithm/L21 Priority queue, Heap/L21 Priority queue, Heap|MinPQ]]。
- Top-M filtering：解决数据流很大但只保留前 M 个的问题；核心思想是超过 M 个元素就移除最小值；相关概念：[[3. DataStructure and Algorithm/L21 Priority queue, Heap/L21 Priority queue, Heap|top-M]]。
- Dijkstra：解决非负边权最短路径；核心思想是 PQ 每次弹出当前 distTo 最小的顶点；相关概念：[[3. DataStructure and Algorithm/L24 Shotest Path/L24 Shotest Path|dijkstra]]、[[graph]]。
- Prim：解决 MST 中每次选择最小 crossing edge；核心思想是用 PQ 管理候选边或顶点；相关概念：[[3. DataStructure and Algorithm/L25 Minimum Spinning Tree/L25 Minimum Spinning Tree|prim-algorithm]]。

## 容易混淆点

- priority queue vs queue：queue 按进入顺序，priority queue 按优先级。
- priority queue vs heap：前者是 ADT，后者是常见实现。
- getSmallest vs removeSmallest：前者只查看，后者改变结构。
- Dijkstra vs Prim：二者都用 PQ，但一个维护源点距离，一个维护当前生成树的 crossing edge。
- decreasePriority vs add duplicate：笔记提到 decreasePriority，具体实现细节需要人工补充。

## 相关概念

- [[heap]]
- [[graph]]
- [[complexity-analysis]]
- [[3. DataStructure and Algorithm/L24 Shotest Path/L24 Shotest Path|dijkstra]]
- [[3. DataStructure and Algorithm/L25 Minimum Spinning Tree/L25 Minimum Spinning Tree|prim-algorithm]]

## 跨课程连接

- CS61A：连接抽象数据类型。
- CSAPP：系统调度可作弱连接，需要人工补充。
- Machine Learning：beam search、top-k 可连接 priority queue。
- UMich DL：search / sampling 中的 top-k 有弱连接，需要人工补充。
