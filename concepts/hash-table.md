---
type: concept
course: CS61B
priority: A
status: draft
aliases: []
related:
  - "[[adt]]"
  - "[[array-list]]"
  - "[[complexity-analysis]]"
  - "[[binary-search-tree]]"
  - "[[graph]]"
---

# Hash Table

## 一句话定义

[[hash-table]] 是把 key 通过 hashCode 映射到 bucket，再在 bucket 内查找元素的数据结构。它在 CS61B 中解决的问题是：不依赖 key 的全局可比较顺序，也能在平均意义上快速完成 contains、add、get 等操作。

## 核心思想

BST 依赖可比较关系，查找成本受树高影响。Hash table 换一个模型：先用 hashCode 把元素分类到桶，再只在对应桶里查找。若 hash 分布均匀且桶数量随元素数量增长，平均桶长可控，查找就接近常数时间。

正确性不只靠 hashCode。HashSet 的 contains 过程是先用 `hashCode()` 找桶，再用 `equals()` 判断桶内哪个对象相等。因此 equals 和 hashCode 必须配套：如果两个对象被 equals 认为相等，它们必须能被带到一致的桶里。可变 key 会破坏这一点，因为对象放入后内容变化可能改变 hashCode，但表不会自动搬桶。

## 核心边界 / Contract / Invariant

核心 invariant 是：每个元素必须位于由当前 hash 规则决定的 bucket 中；bucket 内用 equals 判定对象相等；当平均 bucket 大小超过阈值时，通过 resizing 增加桶数并重新分布元素。

这个 invariant 保证查找会去正确桶。如果 hashCode 与 equals 不一致，contains 可能根本不会检查到真正相等的对象；如果 key 入表后被修改，元素可能留在旧桶，导致之后按新 hash 查找失败；如果桶过长，性能会退化到线性。

## 在 CS61B 中的位置

[[hash-table]] 是 [[binary-search-tree]] 之后的另一条 search/indexing 路线。它连接 [[3. DataStructure and Algorithm/L20 Hashing II/L20 Hashing II|equals]]、[[3. DataStructure and Algorithm/L20 Hashing II/L20 Hashing II|hashcode]]、[[3. DataStructure and Algorithm/L19 Hashing I/L19 Hashing I|resizing]]、[[3. DataStructure and Algorithm/L19 Hashing I/L19 Hashing I|collision]] 和 [[3. DataStructure and Algorithm/L16 Extends, Sets, Maps, and BSTs/L16 Extends, Sets, Maps, and BSTs|map]] / [[3. DataStructure and Algorithm/L16 Extends, Sets, Maps, and BSTs/L16 Extends, Sets, Maps, and BSTs|set]]，也为理解 Trie child map、HashSet、HashMap 这类结构提供基础。

## 典型实现

- HashSet：解决无序集合 membership 查询；核心思想是 hashCode 定位 bucket，equals 判断桶内相等；相关概念：[[3. DataStructure and Algorithm/L19 Hashing I/L19 Hashing I|hash-set]]、[[3. DataStructure and Algorithm/L20 Hashing II/L20 Hashing II|equals-hashcode-contract]]。
- bucket array with chaining：解决多个元素进入同一分类的问题；核心思想是每个 bucket 存一组元素，发生 collision 后在桶内继续查找；相关概念：[[3. DataStructure and Algorithm/L19 Hashing I/L19 Hashing I|bucket]]、[[3. DataStructure and Algorithm/L19 Hashing I/L19 Hashing I|collision]]。
- resizing hash table：解决平均桶长过大的问题；核心思想是 load factor 超过阈值后增加 bucket 数并重分布；相关概念：[[3. DataStructure and Algorithm/L19 Hashing I/L19 Hashing I|resizing]]、[[3. DataStructure and Algorithm/渐进分析/L14 渐进分析3/L14 渐进分析3|amortized-analysis]]。
- Trie child map：解决字符子链接存储过多空位的问题；核心思想可用 HashMap 或 BST 改进 child links；相关概念：[[3. DataStructure and Algorithm/L28 Tries/L28 Tries|trie]]、[[3. DataStructure and Algorithm/L28 Tries/L28 Tries|hash-map]]。

## 容易混淆点

- hashCode vs equals：hashCode 决定去哪个桶，equals 决定桶中哪个对象相等。
- average constant time vs worst case：hash 分布坏或所有元素进同一桶时会退化。
- bucket vs collision：bucket 是分类位置，collision 是多个 key 落入同一位置。
- resizing array vs hash resizing：二者都扩容复制，但 hash table 还要重新按桶规则分布。
- mutable key vs immutable key：可变 key 入表后修改内容会破坏查找路径。

## 相关概念

- [[3. DataStructure and Algorithm/L20 Hashing II/L20 Hashing II|hashcode]]
- [[3. DataStructure and Algorithm/L20 Hashing II/L20 Hashing II|equals]]
- [[3. DataStructure and Algorithm/L20 Hashing II/L20 Hashing II|equals-hashcode-contract]]
- [[3. DataStructure and Algorithm/L19 Hashing I/L19 Hashing I|bucket]]
- [[3. DataStructure and Algorithm/L19 Hashing I/L19 Hashing I|collision]]
- [[3. DataStructure and Algorithm/L19 Hashing I/L19 Hashing I|resizing]]
- [[3. DataStructure and Algorithm/L19 Hashing I/L19 Hashing I|hash-set]]
- [[3. DataStructure and Algorithm/L28 Tries/L28 Tries|hash-map]]

## 跨课程连接

- CS61A：连接 dictionary / table 的查找抽象。
- CSAPP：连接哈希索引、地址和内存定位。
- Machine Learning：连接 feature hashing、embedding lookup，但需要人工补充具体例子。
- UMich DL：连接 embedding table / indexing，但需要人工补充具体例子。
