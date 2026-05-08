# CS61B Index

## 1. 课程主线

CS61B 的主线不是“学一堆数据结构”，而是从 Java 的类型系统和对象模型出发，逐步建立“接口定义行为、实现隐藏细节、复杂度约束设计”的工程化思维。

第一阶段是 Java 基础与对象模型：从 `.java` 编译运行、静态类型、对象创建、`static` 方法、引用类型和值传递开始，理解 Java 中变量保存的是 bits，引用保存的是对象地址。`==`、`equals`、数组、泛型容器、`Map` 等概念都围绕“类型约束”和“对象身份”展开。相关入口：[[1. Introduction to Java/L1 Intro/L1 Intro|L1 Intro]]、[[1. Introduction to Java/L2 Java base/L2 Java base|L2 Java base]]、[[1. Introduction to Java/L3 Reference Recursion intList/L3 Reference Recursion intList|L3 Reference / IntList]]。

第二阶段是从 ADT 到具体实现。笔记从 `IntList` 到 `SLList`，再到双向链表、数组列表，核心变化是抽象屏障逐渐变强：用户不应该直接操作节点、数组或内部指针，而应该通过稳定的方法使用数据结构。`private`、内部类、哨兵节点、缓存 `size`、维护 `last` 指针，都是为了让实现满足清晰 invariant，同时改善性能。相关入口：[[1. Introduction to Java/L4 SLList/L4 SLList|L4 SLList]]、[[1. Introduction to Java/L5 List/L5 List|L5 List]]、[[2. Scope, Static, Linked Lists, Arrays/L7 ArrayLists, Resizing/L7 ArrayLists, Resizing|L7 AList / Resizing]]。

第三阶段是接口、继承、多态和泛型。`interface` 把“能做什么”从“怎么做”里抽出来，`overriding`、默认方法、向上转型、`Comparator` / `Comparable`、泛型静态方法和 bounded type parameters，让同一套算法可以作用在不同实现上。这里开始出现 CS61B 很重要的设计风格：用 ADT 写客户端代码，用具体类承担性能和存储细节。相关入口：[[2. Scope, Static, Linked Lists, Arrays/L8 Interface and Implementation Inheritance/L8 Interface and Implementation Inheritance|L8 Interface / Inheritance]]、[[2. Scope, Static, Linked Lists, Arrays/L9 Subtype Polymorphism, Comparators, Comparables, Generic Functions/L9 Subtype Polymorphism, Comparators, Comparables, Generic Functions|L9 Polymorphism / Generics]]。

第四阶段是复杂度分析与工程化选择。渐进分析把“程序跑得快不快”转化为增长阶、最坏情况、上下界和摊还分析。数组扩容中“每次 + 常数”和“每次乘常数”的差异，说明实现策略会直接改变长期成本。排序部分进一步把算法选择和信息下界联系起来：比较排序受决策树下界限制，而 counting / radix sort 通过改变问题模型突破比较排序下界。相关入口：[[3. DataStructure and Algorithm/渐进分析/L11 渐进分析1/L11 渐进分析1|L11 渐进分析]]、[[3. DataStructure and Algorithm/渐进分析/L14 渐进分析3/L14 渐进分析3|L14 摊还与递归分析]]、[[4. Sort/L34 Sorting and Algorithmic Bounds/L34 Sorting and Algorithmic Bounds|L34 Sorting Bounds]]。

第五阶段是从线性结构进入树、哈希、堆、并查集和图。BST 用有序 invariant 换取对数查找；B-tree 与 LLRB 解决 BST 退化问题；HashSet 用桶、`hashCode`、`equals` 和 resizing 追求平均常数时间；Heap 用 complete tree 与 heap property 支持优先队列；UnionFind 用树、weighted union、path compression 支持近似常数的连通性查询；图则用邻接表、DFS/BFS、Dijkstra、Prim、Kruskal、拓扑排序等把数据结构和算法组合起来。相关入口：[[3. DataStructure and Algorithm/L16 Extends, Sets, Maps, and BSTs/L16 Extends, Sets, Maps, and BSTs|L16 BST]]、[[3. DataStructure and Algorithm/L19 Hashing I/L19 Hashing I|L19 Hashing I]]、[[3. DataStructure and Algorithm/L21 Priority queue, Heap/L21 Priority queue, Heap|L21 Heap]]、[[3. DataStructure and Algorithm/L15 Disjoint Set/L15 Disjoint Set|L15 Disjoint Set]]、[[3. DataStructure and Algorithm/L23 BFS, DFS and implementations/L23 BFS, DFS and implementations|L23 Graph Traversal]]。

项目层面的完整架构笔记不足，未看到专门的 project architecture 总结。但现有笔记已经反复体现了项目设计思想：隐藏内部表示、维护 invariant、把 ADT 和实现分离、把图这种基础数据结构与 BFS/DFS/Dijkstra/MST 等算法类分开，让上层代码依赖稳定接口而不是依赖存储细节。

## 2. 核心概念列表

- Java syntax / OOP：[[java-syntax]]、[[oop]]、[[static-type]]、[[reference-type]]、[[object-creation]]、[[static-method]]。笔记依据充分，主要来自 L1-L3。
- interface / inheritance / polymorphism：[[interface]]、[[inheritance]]、[[implementation-inheritance]]、[[subtype-polymorphism]]、[[upcasting]]、[[overriding]]、[[overloading]]。笔记依据充分，主要来自 L8、L9、L16。
- generics：[[generics]]、[[diamond-syntax]]、[[bounded-type-parameter]]、[[comparable]]、[[comparator]]。笔记依据充分，但泛型擦除、wildcard 等未出现，后续可人工补充。
- iterator / iterable：[[iterator]]、[[iterable]]。需要人工补充；现有 Markdown 只在复习笔记中把 `iterator()` 列为 BST 方法，L10 标题涉及 Iterators，但正文没有完整展开。
- list / linked list / array list：[[list-adt]]、[[intlist]]、[[sllist]]、[[linked-list]]、[[doubly-linked-list]]、[[array-list]]、[[sentinel-node]]、[[resizing-array]]。笔记依据充分，主要来自 L3-L5、L7、L14。
- deque：[[deque]]。需要人工补充；笔记有双向链表、哨兵节点、`prev` / `next` 设计基础，但没有明确讨论 Deque ADT 或完整操作集合。
- tree / binary tree / BST：[[tree]]、[[binary-tree]]、[[binary-search-tree]]、[[tree-traversal]]、[[preorder-traversal]]、[[inorder-traversal]]、[[postorder-traversal]]、[[predecessor-successor]]。笔记依据充分，主要来自 L16、L17、L22、L25.5。
- balanced trees：[[b-tree]]、[[two-three-tree]]、[[red-black-tree]]、[[llrb]]、[[tree-rotation]]。笔记依据充分，主要来自 L17、L18。
- hash table：[[hash-table]]、[[hash-set]]、[[hash-map]]、[[bucket]]、[[collision]]、[[resizing]]、[[hashcode]]、[[equals]]、[[mutable-key]]。笔记依据充分，主要来自 L19、L20。
- priority queue / heap：[[priority-queue]]、[[heap]]、[[binary-heap]]、[[min-heap]]、[[heap-invariant]]、[[array-backed-heap]]。笔记依据充分，主要来自 L21、排序中的 heap sort。
- graph：[[graph]]、[[adjacency-list]]、[[dfs]]、[[bfs]]、[[edge-to]]、[[shortest-path]]、[[dijkstra]]、[[minimum-spanning-tree]]、[[prim-algorithm]]、[[kruskal-algorithm]]、[[topological-sort]]、[[dag]]。笔记依据充分，主要来自 L22-L26。
- union find：[[union-find]]、[[disjoint-set]]、[[weighted-quick-union]]、[[path-compression]]、[[inverse-ackermann]]。笔记依据充分，主要来自 L15、L25。
- asymptotic analysis：[[asymptotic-analysis]]、[[theta-notation]]、[[big-o]]、[[big-omega]]、[[amortized-analysis]]、[[recursion-tree]]、[[decision-tree-lower-bound]]。笔记依据充分，主要来自 L11、L13、L14、L34。
- testing / debugging：[[testing]]、[[debugging]]。需要人工补充；L6 只有 Testing 标题和“见 Coding in Class”，没有系统测试模式或调试策略。
- equals / hashCode：[[equals]]、[[hashcode]]、[[equals-hashcode-contract]]、[[hashset-contains]]。笔记依据充分，主要来自 L3、L10、L20。
- project architecture：[[project-architecture]]、[[abstraction-barrier]]、[[adt]]、[[separation-of-concerns]]。需要人工补充；现有笔记有抽象屏障、图数据结构与算法分离等设计思想，但没有项目结构级别总结。

## 3. 重要代码实现 / 数据结构实现

- SLList / IntNode
  - 解决的问题：把递归裸链表 `IntList` 封装成用户可用的列表，避免客户端直接操作节点。
  - 核心 invariant / 关键思想：`first` 指向链表首节点；`IntNode` 可以作为内部类并设为 `private`；对外暴露 `addFirst`、`getFirst`、`addLast` 等方法形成抽象屏障。
  - 相关概念链接：[[linked-list]]、[[abstraction-barrier]]、[[private]]、[[inner-class]]、[[sllist]]。
  - 来源：[[1. Introduction to Java/L4 SLList/L4 SLList|L4 SLList]]。

- Sentinel SLList / size 缓存
  - 解决的问题：避免空链表和非空链表的特殊判断，并让 `size` 查询不必每次遍历。
  - 核心 invariant / 关键思想：使用哨兵节点统一 null 与普通节点处理；维护 `size` 字段，用空间换时间。
  - 相关概念链接：[[sentinel-node]]、[[invariant]]、[[space-time-tradeoff]]。
  - 来源：[[1. Introduction to Java/L4 SLList/L4 SLList|L4 SLList]]。

- DLList / doubly linked list
  - 解决的问题：单向链表维护 `last` 后仍难以高效删除末尾节点，因为节点不知道前驱。
  - 核心 invariant / 关键思想：每个节点保存 `prev` 和 `next`；可以用一个循环哨兵节点同时服务头尾操作。
  - 相关概念链接：[[doubly-linked-list]]、[[prev-next-links]]、[[sentinel-node]]。
  - 来源：[[1. Introduction to Java/L5 List/L5 List|L5 List]]。

- AList / resizing array list
  - 解决的问题：链表随机访问慢，数组连续存储可以让 `get` 更快。
  - 核心 invariant / 关键思想：用户不应知道底层数组；数组长度固定，需要扩容；乘法扩容比每次加常数扩容有更好的摊还表现。
  - 相关概念链接：[[array-list]]、[[resizing-array]]、[[amortized-analysis]]、[[abstraction-barrier]]。
  - 来源：[[2. Scope, Static, Linked Lists, Arrays/L7 ArrayLists, Resizing/L7 ArrayLists, Resizing|L7 AList]]、[[3. DataStructure and Algorithm/渐进分析/L14 渐进分析3/L14 渐进分析3|L14 摊还分析]]。

- Deque
  - 解决的问题：需要人工补充。
  - 核心 invariant / 关键思想：需要人工补充。现有笔记有双向链表和哨兵节点基础，但没有明确讨论 Deque ADT 的完整实现。
  - 相关概念链接：[[deque]]、[[doubly-linked-list]]、[[sentinel-node]]。

- BST / Map by ordered keys
  - 解决的问题：有序链表 `contains` 和 `add` 是线性时间；BST 用比较关系组织 key，期望对数时间查找、插入、删除。
  - 核心 invariant / 关键思想：左子树 key 小于当前节点，右子树 key 大于当前节点；元素大小关系必须可传递且不允许重复 key；删除两个子节点的节点时使用前驱或后继替换。
  - 相关概念链接：[[binary-search-tree]]、[[map]]、[[predecessor-successor]]、[[tree-invariant]]。
  - 来源：[[3. DataStructure and Algorithm/L16 Extends, Sets, Maps, and BSTs/L16 Extends, Sets, Maps, and BSTs|L16 BST]]、[[3. DataStructure and Algorithm/L25.5 复习/L25.5 复习#BST|L25.5 BST 复习]]。

- B-tree
  - 解决的问题：普通 BST 会因插入顺序退化成链表；B-tree 在任意插入顺序下保持平衡。
  - 核心 invariant / 关键思想：每个节点可容纳多个 key；有 `k` 个元素的非叶节点有 `k+1` 个子节点；所有叶子到 root 距离相同；节点满时把中位数提升并拆分区间。
  - 相关概念链接：[[b-tree]]、[[two-three-tree]]、[[balanced-tree]]。
  - 来源：[[3. DataStructure and Algorithm/L17 B-trees/L17 B-trees|L17 B-trees]]。

- LLRB / left-leaning red-black tree
  - 解决的问题：用普通 BST 结构模拟 2-3 tree 的平衡性。
  - 核心 invariant / 关键思想：红边表示 2-3 tree 中绑定的节点；红边只允许左倾；右红边左旋，连续左红边右旋，左右都红则颜色翻转。
  - 相关概念链接：[[red-black-tree]]、[[llrb]]、[[tree-rotation]]、[[balanced-tree]]。
  - 来源：[[3. DataStructure and Algorithm/L18 Red Black Trees/L18 Red Black Trees|L18 Red Black Trees]]。

- HashSet / Hash table
  - 解决的问题：BST 依赖可比较关系且仍是对数级；HashSet 用分类和桶追求平均常数时间。
  - 核心 invariant / 关键思想：`hashCode` 决定去哪个桶，`equals` 决定桶中哪个元素相等；桶平均长度过大时扩容；坏的 hash 会退化成线性结构；可变 key 会破坏桶位置。
  - 相关概念链接：[[hash-table]]、[[hash-set]]、[[bucket]]、[[collision]]、[[resizing]]、[[equals-hashcode-contract]]、[[mutable-key]]。
  - 来源：[[3. DataStructure and Algorithm/L19 Hashing I/L19 Hashing I|L19 Hashing I]]、[[3. DataStructure and Algorithm/L20 Hashing II/L20 Hashing II|L20 Hashing II]]。

- PriorityQueue / binary heap
  - 解决的问题：需要高效获取、删除最小或最大元素，例如保留前 M 个高能粒子。
  - 核心 invariant / 关键思想：binary min-heap 是 complete binary tree，且每个节点小于等于子节点；`getSmallest` 看 root，`add` swim，`removeSmallest` 把最后节点放到 root 后 sink；数组下标可隐含父子关系。
  - 相关概念链接：[[priority-queue]]、[[heap]]、[[binary-heap]]、[[complete-tree]]、[[heap-invariant]]。
  - 来源：[[3. DataStructure and Algorithm/L21 Priority queue, Heap/L21 Priority queue, Heap|L21 Priority Queue / Heap]]。

- UnionFind / weighted quick union with path compression
  - 解决的问题：动态判断两个元素是否属于同一个集合，支持连通性查询。
  - 核心 invariant / 关键思想：每个集合是一棵树；`isConnected` 判断根是否相同；连接时根连根，小树接大树；查询路径上的节点顺手接到 root，降低后续成本。
  - 相关概念链接：[[union-find]]、[[disjoint-set]]、[[weighted-quick-union]]、[[path-compression]]。
  - 来源：[[3. DataStructure and Algorithm/L15 Disjoint Set/L15 Disjoint Set|L15 Disjoint Set]]。

- Graph adjacency list
  - 解决的问题：图的表示决定算法复杂度；邻接矩阵访问边快但输出所有边不合适，邻接列表适合遍历。
  - 核心 invariant / 关键思想：图数据结构只提供原子操作，BFS/DFS 等算法放在独立类中；邻接列表遍历所有边和点为 `Theta(V + E)`。
  - 相关概念链接：[[graph]]、[[adjacency-list]]、[[separation-of-concerns]]。
  - 来源：[[3. DataStructure and Algorithm/L23 BFS, DFS and implementations/L23 BFS, DFS and implementations|L23 Graph Implementations]]。

- DFS / BFS traversal
  - 解决的问题：在图中搜索可达性、路径和无权最短路径。
  - 核心 invariant / 关键思想：DFS 维护当前递归路径和 marked 状态，`edgeTo` 记录路径来源；BFS 使用队列逐层扩展，`distTo` 每层加 1，因此适合无权最短路径。
  - 相关概念链接：[[dfs]]、[[bfs]]、[[edge-to]]、[[graph-traversal]]。
  - 来源：[[3. DataStructure and Algorithm/L22 Tree and Graph Traversals/L22 Tree and Graph Traversals|L22 Traversals]]、[[3. DataStructure and Algorithm/L23 BFS, DFS and implementations/L23 BFS, DFS and implementations|L23 BFS / DFS]]。

- Dijkstra shortest path
  - 解决的问题：BFS 不能处理有权图，因为它把所有边权视为相同。
  - 核心 invariant / 关键思想：维护当前已知 `distTo`；每次从优先队列弹出最小距离顶点并松弛邻边；正确性依赖非负边权。
  - 相关概念链接：[[dijkstra]]、[[shortest-path]]、[[priority-queue]]、[[relaxation]]。
  - 来源：[[3. DataStructure and Algorithm/L24 Shotest Path/L24 Shotest Path|L24 Shortest Path]]。

- MST: Prim / Kruskal
  - 解决的问题：在无向带权图中找到边权和最小、连通且无环的生成树。
  - 核心 invariant / 关键思想：cut property 保证任意 cut 的最小 crossing edge 在 MST 中；Prim 用优先队列维护当前 cut 边；Kruskal 按边权排序并用 UnionFind 跳过成环边。
  - 相关概念链接：[[minimum-spanning-tree]]、[[cut-property]]、[[prim-algorithm]]、[[kruskal-algorithm]]、[[union-find]]。
  - 来源：[[3. DataStructure and Algorithm/L25 Minimum Spinning Tree/L25 Minimum Spinning Tree|L25 Minimum Spanning Tree]]。

- DAG topological sort
  - 解决的问题：在有先修依赖的有向无环图中给出可执行顺序，并支持 DAG 上的最短/最长路径思路。
  - 核心 invariant / 关键思想：只有 DAG 能拓扑排序；DFS 后序反转可得到拓扑序；拓扑序中每条边都朝向顺序后方。
  - 相关概念链接：[[dag]]、[[topological-sort]]、[[dfs]]。
  - 来源：[[3. DataStructure and Algorithm/L26 Directed Acyclic Graphs/L26 Directed Acyclic Graphs|L26 DAGs]]。

- Trie / TrieMap
  - 解决的问题：高效存储字符串集合和前缀查询。
  - 核心 invariant / 关键思想：路径表示字符串，节点共享前缀；需要标记单词结尾；TrieMap 在结尾节点放 value；`DataIndexedCharMap` 用字符索引子链接，但可能产生大量空链接，可用 HashMap 或 BST 改进。
  - 相关概念链接：[[trie]]、[[trie-map]]、[[prefix-query]]、[[hash-map]]。
  - 来源：[[3. DataStructure and Algorithm/L28 Tries/L28 Tries|L28 Tries]]。

- Iterator / Iterable
  - 解决的问题：需要人工补充。
  - 核心 invariant / 关键思想：需要人工补充；现有笔记没有完整说明 `Iterator` 状态、`hasNext` / `next` 契约或 `Iterable` 与增强 for 循环关系。
  - 相关概念链接：[[iterator]]、[[iterable]]。

- equals / hashCode
  - 解决的问题：让对象相等性和哈希容器查找一致。
  - 核心 invariant / 关键思想：默认 `equals` 类似 `==`；重写 `equals` 时必须配套重写 `hashCode`；HashSet 先按 `hashCode` 找桶，再用 `equals` 判断桶内元素。
  - 相关概念链接：[[equals]]、[[hashcode]]、[[equals-hashcode-contract]]、[[hashset-contains]]。
  - 来源：[[2. Scope, Static, Linked Lists, Arrays/L10 Iterators, Object Methods/L10 Iterators, Object Methods|L10 Object Methods]]、[[3. DataStructure and Algorithm/L20 Hashing II/L20 Hashing II|L20 Hashing II]]。

- Testing patterns
  - 解决的问题：需要人工补充。
  - 核心 invariant / 关键思想：需要人工补充；L6 只有 Testing 标题和“见 Coding in Class”，缺少 JUnit、edge cases、randomized testing、integration tests 等系统内容。
  - 相关概念链接：[[testing]]、[[debugging]]。

## 4. 容易混淆点

- interface vs abstract class：[[interface]] 有笔记依据；[[abstract-class]] 需要人工补充。现有笔记强调 interface 定义标准、不能实例化、可有 default method，但没有系统讨论 abstract class。
- overloading vs overriding：[[overloading]] 是同名方法、参数列表不同；[[overriding]] 是子类中完全相同 signature 的方法重写。来源：L8。
- == vs equals：== 比较引用或基本值；默认 [[equals]] 如果不重写，效果接近 `==`。来源：L3、L10。
- equals vs hashCode：[[hashcode]] 决定去哪个桶，[[equals]] 决定桶中哪个对象相等；重写 equals 必须配套 hashCode。来源：L20。
- Iterable vs Iterator：[[iterable]] / [[iterator]] 需要人工补充；笔记未充分展开。
- ArrayList vs LinkedList：[[array-list]] 用连续数组换取快速随机访问，但需要 resizing；[[linked-list]] 用节点连接，插入删除位置相关，随机访问慢。来源：L5、L7。
- SLList sentinel vs null special case：[[sentinel-node]] 用统一节点模型减少空表分支；普通 null 头节点需要额外判断。来源：L4。
- BST invariant vs heap invariant：[[binary-search-tree]] 约束左小右大，支持 search；[[heap]] 只保证父节点不大于子节点，root 最小，但左右子树之间无全局排序。来源：L16、L21。
- BFS vs DFS：[[bfs]] 使用队列逐层扩展，适合无权最短路径；[[dfs]] 沿路径深入，适合可达性、路径、后序等结构性处理。来源：L22、L23。
- tree recursion vs graph traversal：[[tree-traversal]] 默认没有环；[[graph-traversal]] 必须 marked / visited，否则可能重复访问或陷入环。来源：L22。
- HashMap bucket / collision / resizing：[[bucket]] 是 hash 后的分类位置；[[collision]] 是多个元素进同一桶；[[resizing]] 用更大的桶数组控制平均桶长。来源：L19。
- static type vs dynamic type：[[static-type]] 在编译期约束能调用什么；[[dynamic-type]] 与多态分派相关。现有笔记有静态类型、向上转型、多态，但 static/dynamic type 对照需要人工补充。
- Comparable vs Comparator：[[comparable]] 是对象自身可比较；[[comparator]] 是外部比较规则。来源：L9。
- mutable key vs hash container：[[mutable-key]] 放入 HashSet / HashMap 后如果内容改变，hashCode 可能变，元素仍留在旧桶，导致查找失败。来源：L20。
- BFS shortest path vs Dijkstra：[[bfs]] 只适合无权或等权图；[[dijkstra]] 用优先队列和松弛处理非负带权图。来源：L24。
- Prim vs Dijkstra：二者都用 [[priority-queue]]，但 [[prim-algorithm]] 关心当前生成树到外部的最小 crossing edge，[[dijkstra]] 关心从源点到顶点的最短距离。来源：L25。

## 5. 推荐复习顺序

第一轮：Java / OOP / 测试基础
- 核心概念：[[java-syntax]]、[[static-type]]、[[reference-type]]、[[oop]]、[[static-method]]、[[equals]]、[[interface]]、[[inheritance]]、[[polymorphism]]、[[generics]]、[[testing]]。
- 相关入口：[[1. Introduction to Java/L1 Intro/L1 Intro|L1 Intro]]、[[1. Introduction to Java/L2 Java base/L2 Java base|L2 Java base]]、[[1. Introduction to Java/L3 Reference Recursion intList/L3 Reference Recursion intList|L3 Reference]]、[[2. Scope, Static, Linked Lists, Arrays/L8 Interface and Implementation Inheritance/L8 Interface and Implementation Inheritance|L8 Interface]]、[[2. Scope, Static, Linked Lists, Arrays/L9 Subtype Polymorphism, Comparators, Comparables, Generic Functions/L9 Subtype Polymorphism, Comparators, Comparables, Generic Functions|L9 Polymorphism / Generics]]、[[2. Scope, Static, Linked Lists, Arrays/L10 Iterators, Object Methods/L10 Iterators, Object Methods|L10 Object Methods]]、[[2. Scope, Static, Linked Lists, Arrays/L6 Testing/L6 Testing|L6 Testing]]。
- 注意：testing/debugging 需要人工补充。

第二轮：线性数据结构
- 核心概念：[[adt]]、[[abstraction-barrier]]、[[intlist]]、[[sllist]]、[[linked-list]]、[[doubly-linked-list]]、[[sentinel-node]]、[[array-list]]、[[resizing-array]]、[[amortized-analysis]]。
- 相关入口：[[1. Introduction to Java/L3 Reference Recursion intList/L3 Reference Recursion intList|L3 IntList]]、[[1. Introduction to Java/L4 SLList/L4 SLList|L4 SLList]]、[[1. Introduction to Java/L5 List/L5 List|L5 List]]、[[2. Scope, Static, Linked Lists, Arrays/L7 ArrayLists, Resizing/L7 ArrayLists, Resizing|L7 AList]]、[[3. DataStructure and Algorithm/渐进分析/L14 渐进分析3/L14 渐进分析3|L14 Resizing Analysis]]。
- 注意：Deque 需要人工补充。

第三轮：树与递归结构
- 核心概念：[[tree]]、[[binary-tree]]、[[binary-search-tree]]、[[tree-traversal]]、[[predecessor-successor]]、[[b-tree]]、[[llrb]]、[[tree-rotation]]、[[trie]]。
- 相关入口：[[3. DataStructure and Algorithm/L16 Extends, Sets, Maps, and BSTs/L16 Extends, Sets, Maps, and BSTs|L16 BST]]、[[3. DataStructure and Algorithm/L17 B-trees/L17 B-trees|L17 B-trees]]、[[3. DataStructure and Algorithm/L18 Red Black Trees/L18 Red Black Trees|L18 Red Black Trees]]、[[3. DataStructure and Algorithm/L22 Tree and Graph Traversals/L22 Tree and Graph Traversals|L22 Tree Traversals]]、[[3. DataStructure and Algorithm/L28 Tries/L28 Tries|L28 Tries]]。

第四轮：哈希、堆、并查集
- 核心概念：[[hash-table]]、[[hash-set]]、[[hashcode]]、[[equals-hashcode-contract]]、[[mutable-key]]、[[priority-queue]]、[[heap]]、[[union-find]]、[[path-compression]]。
- 相关入口：[[3. DataStructure and Algorithm/L19 Hashing I/L19 Hashing I|L19 Hashing I]]、[[3. DataStructure and Algorithm/L20 Hashing II/L20 Hashing II|L20 Hashing II]]、[[3. DataStructure and Algorithm/L21 Priority queue, Heap/L21 Priority queue, Heap|L21 Heap]]、[[3. DataStructure and Algorithm/L15 Disjoint Set/L15 Disjoint Set|L15 Disjoint Set]]。

第五轮：图算法与综合项目
- 核心概念：[[graph]]、[[adjacency-list]]、[[dfs]]、[[bfs]]、[[shortest-path]]、[[dijkstra]]、[[minimum-spanning-tree]]、[[prim-algorithm]]、[[kruskal-algorithm]]、[[dag]]、[[topological-sort]]、[[project-architecture]]。
- 相关入口：[[3. DataStructure and Algorithm/L22 Tree and Graph Traversals/L22 Tree and Graph Traversals|L22 Graph Traversals]]、[[3. DataStructure and Algorithm/L23 BFS, DFS and implementations/L23 BFS, DFS and implementations|L23 BFS / DFS]]、[[3. DataStructure and Algorithm/L24 Shotest Path/L24 Shotest Path|L24 Shortest Path]]、[[3. DataStructure and Algorithm/L25 Minimum Spinning Tree/L25 Minimum Spinning Tree|L25 MST]]、[[3. DataStructure and Algorithm/L26 Directed Acyclic Graphs/L26 Directed Acyclic Graphs|L26 DAGs]]。
- 注意：project architecture 需要人工补充；现有图笔记只提供了“图数据结构与算法类分离”的设计线索。

第六轮：复杂度分析与工程化复盘
- 核心概念：[[asymptotic-analysis]]、[[theta-notation]]、[[big-o]]、[[big-omega]]、[[amortized-analysis]]、[[recursion-tree]]、[[sorting]]、[[comparison-sort-lower-bound]]、[[stable-sort]]、[[radix-sort]]、[[engineering-tradeoff]]。
- 相关入口：[[3. DataStructure and Algorithm/渐进分析/L11 渐进分析1/L11 渐进分析1|L11 渐进分析1]]、[[3. DataStructure and Algorithm/渐进分析/L13 渐进分析2/L13 渐进分析2|L13 渐进分析2]]、[[3. DataStructure and Algorithm/渐进分析/L14 渐进分析3/L14 渐进分析3|L14 渐进分析3]]、[[4. Sort/L28 Sorting1/L28 Sorting1|L28 Sorting]]、[[4. Sort/L30 Merge Sort, Insertion Sort, and Quick Sort/L30 Merge Sort, Insertion Sort, and Quick Sort|L30 Merge / Insertion / Quick]]、[[4. Sort/L33 Quick Sort/L33 Quick Sort|L33 Quick Sort]]、[[4. Sort/L34 Sorting and Algorithmic Bounds/L34 Sorting and Algorithmic Bounds|L34 Sorting Bounds]]、[[4. Sort/L36 Radix Sorting/L36 Radix Sorting|L36 Radix Sorting]]。

## 6. 可抽取到 20_Concepts 的候选条目

- 概念名：abstraction
  - 推荐文件名：`abstraction.md`
  - 优先级：A
  - 为什么值得长期保留：贯穿 SLList、AList、interface、graph implementation，是 CS61B 从写代码走向设计数据结构的核心。
  - 可能连接到的其他课程：CS61A、CSAPP、Machine Learning。

- 概念名：ADT
  - 推荐文件名：`adt.md`
  - 优先级：A
  - 为什么值得长期保留：帮助区分“操作契约”和“底层表示”，是 List、Set、Map、PQ、Graph 的共同基础。
  - 可能连接到的其他课程：CS61A、CSAPP。

- 概念名：interface
  - 推荐文件名：`interface.md`
  - 优先级：A
  - 为什么值得长期保留：连接 OOP、多态、客户端代码复用和工程抽象。
  - 可能连接到的其他课程：CS61A、CSAPP。

- 概念名：generics
  - 推荐文件名：`generics.md`
  - 优先级：A
  - 为什么值得长期保留：让数据结构和算法摆脱具体元素类型，是 Java 容器和比较接口的基础。
  - 可能连接到的其他课程：CS61A。

- 概念名：iterator
  - 推荐文件名：`iterator.md`
  - 优先级：B
  - 为什么值得长期保留：是容器遍历协议的重要概念，但当前笔记内容不足，需要补全。
  - 可能连接到的其他课程：CS61A。

- 概念名：linked-list
  - 推荐文件名：`linked-list.md`
  - 优先级：A
  - 为什么值得长期保留：指针式结构、哨兵节点、抽象屏障、线性结构性能权衡都集中在这里。
  - 可能连接到的其他课程：CS61A、CSAPP。

- 概念名：tree
  - 推荐文件名：`tree.md`
  - 优先级：A
  - 为什么值得长期保留：BST、Heap、UnionFind、Trie、Graph traversal 都借用树的递归结构。
  - 可能连接到的其他课程：CS61A、Machine Learning、UMich DL。

- 概念名：binary-search-tree
  - 推荐文件名：`binary-search-tree.md`
  - 优先级：A
  - 为什么值得长期保留：用 invariant 换取查找效率，是 Map/Set 和平衡树的入口。
  - 可能连接到的其他课程：CS61A、Machine Learning。

- 概念名：hash-table
  - 推荐文件名：`hash-table.md`
  - 优先级：A
  - 为什么值得长期保留：平均常数时间、hashCode/equals 契约、collision 和 resizing 是长期高频概念。
  - 可能连接到的其他课程：CSAPP、Machine Learning。

- 概念名：heap
  - 推荐文件名：`heap.md`
  - 优先级：A
  - 为什么值得长期保留：用弱排序 invariant 支撑高效优先级操作，是排序和图算法的基础。
  - 可能连接到的其他课程：Machine Learning。

- 概念名：priority-queue
  - 推荐文件名：`priority-queue.md`
  - 优先级：A
  - 为什么值得长期保留：Dijkstra、Prim、heap sort 都依赖它，是从数据结构到算法的桥。
  - 可能连接到的其他课程：Machine Learning、UMich DL。

- 概念名：union-find
  - 推荐文件名：`union-find.md`
  - 优先级：A
  - 为什么值得长期保留：weighted union + path compression 是典型的 invariant 和摊还优化案例，也服务 Kruskal。
  - 可能连接到的其他课程：CSAPP、Machine Learning。

- 概念名：graph
  - 推荐文件名：`graph.md`
  - 优先级：A
  - 为什么值得长期保留：BFS、DFS、最短路、MST、DAG 都以图为统一模型。
  - 可能连接到的其他课程：CS61A、Machine Learning、UMich DL。

- 概念名：complexity-analysis
  - 推荐文件名：`complexity-analysis.md`
  - 优先级：A
  - 为什么值得长期保留：所有数据结构选择都需要复杂度语言来表达，包括最坏情况、摊还、下界。
  - 可能连接到的其他课程：CSAPP、Machine Learning、UMich DL。

- 概念名：testing
  - 推荐文件名：`testing.md`
  - 优先级：B
  - 为什么值得长期保留：工程化实现必须配套测试，但当前笔记内容不足，需要补充 JUnit、边界测试和随机测试。
  - 可能连接到的其他课程：CS61A、CSAPP。

- 概念名：equals-hashCode-contract
  - 推荐文件名：`equals-hashCode-contract.md`
  - 优先级：A
  - 为什么值得长期保留：这是 Java 哈希容器正确性的核心，也是容易出错的工程契约。
  - 可能连接到的其他课程：CSAPP。

- 概念名：trie
  - 推荐文件名：`trie.md`
  - 优先级：B
  - 为什么值得长期保留：字符串集合、前缀查询、空间换时间和 Map-backed child links 都很典型。
  - 可能连接到的其他课程：Machine Learning。

## 7. 不要做的事

本索引保持以下边界：不逐文件总结，不生成 `40_Mistakes`，不创建 `20_Concepts` 文件，不修改原始笔记，不补写笔记中没有依据的内容，不把 `index.md` 写成课程目录清单。
