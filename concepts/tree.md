---
type: concept
course: CS61B
priority: A
status: draft
aliases: []
related:
  - "[[linked-list]]"
  - "[[binary-search-tree]]"
  - "[[heap]]"
  - "[[union-find]]"
  - "[[graph]]"
  - "[[dfs]]"
---

# Tree

## 一句话定义

[[tree]] 是用 root、child、leaf 等层级关系组织数据的结构。它在 CS61B 中解决的问题是：把线性序列扩展成递归分支结构，为 BST、B-tree、heap、trie、UnionFind 和遍历算法提供共同模型。

## 核心思想

树的本质是递归结构：一个节点下面挂着若干子树。这个形状让很多操作可以写成“处理当前节点，再处理子树”，例如 preorder、inorder、postorder 或层序遍历。

CS61B 中的树不是单一数据结构，而是一组实现思想。BST 用有序 invariant 支撑查找，B-tree 和 LLRB 维护平衡，heap 用 complete tree 加 heap property 支撑极值操作，UnionFind 用树表示集合，trie 用路径表示字符串前缀。树是进入图之前的关键台阶，因为图可以看作更少限制的节点-边结构，允许环和更自由的连接。

## 核心边界 / Contract / Invariant

树的核心约束是层级父子关系：从 root 出发沿 child 关系访问节点，子结构仍然是树。具体 invariant 取决于树的用途；普通 tree 只表达层级，BST 增加 left < node < right，heap 增加 parent <= children，B-tree 增加所有叶子深度一致。

这个边界保证递归遍历能终止，并让每类树的操作有明确方向。如果树结构被破坏成有环或任意图，普通 tree traversal 可能重复访问或无法终止，必须转向 graph traversal 的 marked / visited 逻辑。

## 在 CS61B 中的位置

[[tree]] 位于线性结构之后、图结构之前。它把 [[linked-list]] 的引用思想推广到分支结构，又为 [[binary-search-tree]]、[[3. DataStructure and Algorithm/L21 Priority queue, Heap/L21 Priority queue, Heap|heap]]、[[3. DataStructure and Algorithm/L15 Disjoint Set/L15 Disjoint Set|union-find]]、[[3. DataStructure and Algorithm/L28 Tries/L28 Tries|trie]] 和 [[3. DataStructure and Algorithm/L22 Tree and Graph Traversals/L22 Tree and Graph Traversals|graph]] traversal 建立递归模型。

## 典型实现

- Binary Search Tree：解决有序 key 的查找、插入和删除；核心思想是 ordered invariant；相关概念：[[binary-search-tree]]、[[3. DataStructure and Algorithm/L17 B-trees/L17 B-trees|predecessor-successor]]。
- B-tree：解决 BST 因插入顺序退化的问题；核心思想是多 key 节点和所有叶子等深；相关概念：[[3. DataStructure and Algorithm/L17 B-trees/L17 B-trees|b-tree]]、[[3. DataStructure and Algorithm/L17 B-trees/L17 B-trees|balanced-tree]]。
- LLRB：解决用普通 BST 形状模拟 2-3 tree 平衡性的问题；核心思想是左倾红边和旋转；相关概念：[[3. DataStructure and Algorithm/L18 Red Black Trees/L18 Red Black Trees|llrb]]、[[3. DataStructure and Algorithm/L18 Red Black Trees/L18 Red Black Trees|tree-rotation]]。
- Heap：解决高效极值访问；核心思想是 complete tree 和 heap property；相关概念：[[3. DataStructure and Algorithm/L21 Priority queue, Heap/L21 Priority queue, Heap|heap]]、[[3. DataStructure and Algorithm/L21 Priority queue, Heap/L21 Priority queue, Heap|priority-queue]]。
- UnionFind forest：解决动态连通性；核心思想是每个集合用一棵树表示；相关概念：[[3. DataStructure and Algorithm/L15 Disjoint Set/L15 Disjoint Set|union-find]]。

## 容易混淆点

- tree vs graph：tree 有层级约束，graph 允许环和任意边。
- binary tree vs BST：binary tree 只限制子节点数量，BST 额外限制 key 的顺序。
- BST invariant vs heap invariant：BST 支持搜索方向，heap 只保证 root 附近的优先级关系。
- depth vs size：深度影响查找成本，节点数不直接等于操作成本。
- tree traversal vs graph traversal：树遍历通常不需要 marked，图遍历必须防止重复访问。

## 相关概念

- [[binary-search-tree]]
- [[3. DataStructure and Algorithm/L22 Tree and Graph Traversals/L22 Tree and Graph Traversals|tree-traversal]]
- [[3. DataStructure and Algorithm/L17 B-trees/L17 B-trees|b-tree]]
- [[3. DataStructure and Algorithm/L18 Red Black Trees/L18 Red Black Trees|llrb]]
- [[3. DataStructure and Algorithm/L21 Priority queue, Heap/L21 Priority queue, Heap|heap]]
- [[3. DataStructure and Algorithm/L15 Disjoint Set/L15 Disjoint Set|union-find]]
- [[3. DataStructure and Algorithm/L22 Tree and Graph Traversals/L22 Tree and Graph Traversals|graph]]

## 跨课程连接

- CS61A：连接 tree recursion 和递归数据结构。
- CSAPP：树形索引或文件系统可作为弱连接，需要人工补充。
- Machine Learning：连接 decision tree 和 search tree。
- UMich DL：computation graph 可用图/树思想连接，但需要人工补充具体例子。
