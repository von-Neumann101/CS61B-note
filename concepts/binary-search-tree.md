---
type: concept
course: CS61B
priority: A
status: draft
aliases: []
related:
  - "[[tree]]"
  - "[[complexity-analysis]]"
  - "[[hash-table]]"
  - "[[generics]]"
---

# Binary Search Tree

## 一句话定义

[[binary-search-tree]] 是带有有序 invariant 的二叉树：左侧 key 小于当前节点，右侧 key 大于当前节点。它在 CS61B 中解决的问题是：用 key 的可比较性组织查找、插入和删除，避免有序链表中线性扫描的成本。

## 核心思想

BST 把比较结果变成搜索方向。查找 key 时，每一步只需要和当前节点比较，小于就进左子树，大于就进右子树。插入也按同样规则一路下降，直到找到空位。

BST 的性能来自高度，而不是节点总数本身。树足够茂密时，查找路径接近对数长度；如果按递增顺序插入，BST 可能退化成链表，最坏情况变成线性时间。因此 B-tree 和 LLRB 都是在保留 ordered search 思想的同时，额外维护平衡。

## 核心边界 / Contract / Invariant

核心 invariant 是：任意节点的左子树所有 key 都小于该节点 key，右子树所有 key 都大于该节点 key；笔记中强调 BST 不允许重复元素，且任意两个元素之间大小关系必须可传递。

这个 invariant 保证 search、put、contains 能通过比较逐步排除一半方向。删除两个子节点的节点时，必须用前驱或后继替换，才能保持左右区间关系。如果 invariant 被破坏，搜索可能走错方向，即使元素存在也找不到。

## 在 CS61B 中的位置

[[binary-search-tree]] 是从 [[tree]] 进入 ordered map/set 的入口。它承接 Comparable / Comparator 的比较思想，向后连接 [[3. DataStructure and Algorithm/L17 B-trees/L17 B-trees|b-tree]]、[[3. DataStructure and Algorithm/L18 Red Black Trees/L18 Red Black Trees|llrb]]、[[3. DataStructure and Algorithm/L18 Red Black Trees/L18 Red Black Trees|tree-rotation]]，也为理解 hash table 的另一种查找路线提供对照。

## 典型实现

- BST Map：解决 key-value 查询问题；核心思想是用唯一 key 决定左右方向，并把 value 与 key 打包；相关概念：[[3. DataStructure and Algorithm/L16 Extends, Sets, Maps, and BSTs/L16 Extends, Sets, Maps, and BSTs|map]]、[[2. Scope, Static, Linked Lists, Arrays/L9 Subtype Polymorphism, Comparators, Comparables, Generic Functions/L9 Subtype Polymorphism, Comparators, Comparables, Generic Functions|comparable]]。
- BST remove：解决删除节点后保持 ordered invariant；核心思想是按无子节点、一个子节点、两个子节点分情况，两个子节点用前驱或后继替换；相关概念：[[3. DataStructure and Algorithm/L17 B-trees/L17 B-trees|predecessor-successor]]。
- B-tree：解决普通 BST 插入顺序导致退化的问题；核心思想是多元素节点和等深叶子；相关概念：[[3. DataStructure and Algorithm/L17 B-trees/L17 B-trees|b-tree]]。
- LLRB：解决用 BST 结构保持 2-3 tree 平衡性的问题；核心思想是红边、左倾约束和旋转；相关概念：[[3. DataStructure and Algorithm/L18 Red Black Trees/L18 Red Black Trees|llrb]]、[[3. DataStructure and Algorithm/L18 Red Black Trees/L18 Red Black Trees|tree-rotation]]。

## 容易混淆点

- binary tree vs BST：binary tree 只有形状限制，BST 有 key 顺序限制。
- BST invariant vs heap invariant：BST 左右子树全局有序，heap 只要求父子优先级关系。
- predecessor vs successor：前驱是小于当前 key 的最大 key，后继是大于当前 key 的最小 key。
- average height vs worst-case height：随机插入期望较茂密，递增插入可能退化成链表。
- Set vs Map in BST：Set 存 key，Map 用 key 决定位置并关联 value。

## 相关概念

- [[tree]]
- [[3. DataStructure and Algorithm/L16 Extends, Sets, Maps, and BSTs/L16 Extends, Sets, Maps, and BSTs|binary-tree]]
- [[3. DataStructure and Algorithm/L17 B-trees/L17 B-trees|predecessor-successor]]
- [[3. DataStructure and Algorithm/L17 B-trees/L17 B-trees|b-tree]]
- [[3. DataStructure and Algorithm/L18 Red Black Trees/L18 Red Black Trees|llrb]]
- [[3. DataStructure and Algorithm/L18 Red Black Trees/L18 Red Black Trees|tree-rotation]]
- [[2. Scope, Static, Linked Lists, Arrays/L9 Subtype Polymorphism, Comparators, Comparables, Generic Functions/L9 Subtype Polymorphism, Comparators, Comparables, Generic Functions|comparable]]

## 跨课程连接

- CS61A：连接树递归和递归搜索。
- CSAPP：索引结构可作弱连接，需要人工补充。
- Machine Learning：decision tree 搜索有弱连接，需要人工补充。
- UMich DL：连接较弱，需要人工补充。
