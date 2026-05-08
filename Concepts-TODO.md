# CS61B Concepts TODO

## 1. 高优先级概念 A

### [[abstraction]]

- 推荐文件名：abstraction.md
- 来源：CS61B
- 优先级：A
- 为什么重要：贯穿 SLList、AList、interface、graph implementation，是从“写出能跑的代码”进入“设计可维护数据结构”的核心。
- 核心问题：如何隐藏实现细节，只暴露稳定操作，让客户端不依赖节点、数组、桶、邻接表等内部表示。
- 应该包含的内容：抽象屏障、private/internal representation、客户端视角、实现视角、invariant、空间换时间。
- 相关实现：SLList / IntNode、Sentinel SLList、AList、HashSet、Graph adjacency list。
- 相关课程连接：
  - CS61A：data abstraction、ADT、递归结构。
  - CSAPP：内存表示与抽象机器层。
  - Machine Learning：模型接口、数据表示与训练过程分离。
  - UMich DL：模块化网络层与张量操作封装。
- 需要人工补充：可补充项目级 abstraction 示例。

### [[ADT]]

- 推荐文件名：ADT.md
- 来源：CS61B
- 优先级：A
- 为什么重要：List、Set、Map、PriorityQueue、Graph 都应先理解“操作契约”，再理解具体实现。
- 核心问题：一个数据类型应该承诺哪些行为，而不是先关心底层怎么存。
- 应该包含的内容：ADT vs implementation、client code、method contract、List / Set / Map / PQ / Graph 的共同模式。
- 相关实现：List61B、SLList、AList、HashSet、BST Map、PriorityQueue、Graph。
- 相关课程连接：
  - CS61A：抽象数据类型、pair/list/tree。
  - CSAPP：接口与实现分层。
  - Machine Learning：Dataset / Model / Optimizer 的抽象接口。
  - UMich DL：layer、module、loss function 的接口化。
- 需要人工补充：补充更标准的 ADT 定义和操作契约模板。

### [[interface]]

- 推荐文件名：interface.md
- 来源：CS61B
- 优先级：A
- 为什么重要：interface 是 CS61B 中连接抽象、继承、多态和泛型容器的关键语言机制。
- 核心问题：如何用 Java 类型系统表达“这个对象必须支持哪些操作”。
- 应该包含的内容：interface 不能实例化、定义标准、default method、接口继承、向上转型、客户端依赖接口。
- 相关实现：List61B、Set61B、Comparable、Comparator。
- 相关课程连接：
  - CS61A：抽象接口与数据抽象。
  - CSAPP：模块边界与调用契约。
  - Machine Learning：统一模型 API。
  - UMich DL：统一 layer/module API。
- 需要人工补充：abstract class 对比需要补充。

### [[polymorphism]]

- 推荐文件名：polymorphism.md
- 来源：CS61B
- 优先级：A
- 为什么重要：多态让同一个算法可以处理不同具体类，是数据结构客户端代码复用的基础。
- 核心问题：静态类型为接口时，运行时如何调用具体实现。
- 应该包含的内容：subtype polymorphism、upcasting、overriding、接口参数、Comparable / Comparator 使用场景。
- 相关实现：List61B 参数接收 AList、Comparable compareTo、Comparator 外部比较器。
- 相关课程连接：
  - CS61A：通用函数、数据导向编程。
  - CSAPP：动态分派可联系到运行时调用机制。
  - Machine Learning：不同模型共享 predict/train 接口。
  - UMich DL：不同 layer 共享 forward 接口。
- 需要人工补充：static type / dynamic type 的系统对照。

### [[generics]]

- 推荐文件名：generics.md
- 来源：CS61B
- 优先级：A
- 为什么重要：泛型让数据结构和算法摆脱具体元素类型，是 Java 容器实现和比较接口的基础。
- 核心问题：如何写一个对多种类型安全工作的类或方法。
- 应该包含的内容：diamond syntax、泛型类、泛型静态方法、bounded type parameter、`T extends Comparable<T>`。
- 相关实现：List、Map、泛型随机选择函数、Comparable 限制。
- 相关课程连接：
  - CS61A：高阶抽象与通用数据结构。
  - CSAPP：类型系统连接较弱。
  - Machine Learning：泛型思想可连接到通用数据管线。
  - UMich DL：泛化 API 设计。
- 需要人工补充：wildcard、type erasure 没有充分笔记依据。

### [[linked-list]]

- 推荐文件名：linked-list.md
- 来源：CS61B
- 优先级：A
- 为什么重要：链表集中体现引用、节点、递归结构、抽象屏障、哨兵节点和性能权衡。
- 核心问题：如何用节点引用表示线性序列，并通过 invariant 管住指针结构。
- 应该包含的内容：IntList、SLList、DLList、`first`、`last`、`prev` / `next`、sentinel、size 缓存。
- 相关实现：IntList、SLList、Sentinel SLList、DLList。
- 相关课程连接：
  - CS61A：递归 list、pair/list。
  - CSAPP：指针、内存布局、链式结构。
  - Machine Learning：连接较弱。
  - UMich DL：连接较弱。
- 需要人工补充：可补充复杂度表和常见边界条件。

### [[array-list]]

- 推荐文件名：array-list.md
- 来源：CS61B
- 优先级：A
- 为什么重要：ArrayList 是数组存储、随机访问、扩容和摊还分析的核心案例。
- 核心问题：如何用固定长度数组实现逻辑上可增长的 List。
- 应该包含的内容：数组固定长度、`System.arraycopy`、resizing、乘法扩容、摊还成本、和 linked-list 的差异。
- 相关实现：AList / resizing array list。
- 相关课程连接：
  - CS61A：序列抽象。
  - CSAPP：连续内存、缓存局部性。
  - Machine Learning：数组 / tensor 批量存储。
  - UMich DL：tensor contiguous storage 可建立远连接。
- 需要人工补充：AList 的完整方法集合可以补充。

### [[tree]]

- 推荐文件名：tree.md
- 来源：CS61B
- 优先级：A
- 为什么重要：BST、Heap、UnionFind、Trie、DFS/BFS 都依赖树或树式思维。
- 核心问题：如何用层级结构表达递归关系和局部 invariant。
- 应该包含的内容：root、child、leaf、depth、tree traversal、递归处理、树与图的差异。
- 相关实现：BST、B-tree、LLRB、Heap、UnionFind、Trie。
- 相关课程连接：
  - CS61A：tree recursion。
  - CSAPP：树形索引、文件系统有弱连接。
  - Machine Learning：decision tree、search tree。
  - UMich DL：computation graph 可用图/树思想连接。
- 需要人工补充：树的标准术语可补齐。

### [[binary-search-tree]]

- 推荐文件名：binary-search-tree.md
- 来源：CS61B
- 优先级：A
- 为什么重要：BST 是用 ordered invariant 换取查找效率的基础，也是 B-tree、LLRB 的入口。
- 核心问题：如何利用 key 的可比较性组织查找、插入和删除。
- 应该包含的内容：left < node < right、不允许重复 key、search / put / remove、前驱 / 后继、退化情况。
- 相关实现：BST Map、B-tree、LLRB。
- 相关课程连接：
  - CS61A：树递归。
  - CSAPP：索引结构有弱连接。
  - Machine Learning：decision tree 搜索有弱连接。
  - UMich DL：连接较弱。
- 需要人工补充：平衡 BST 的复杂度对比可补充。

### [[hash-table]]

- 推荐文件名：hash-table.md
- 来源：CS61B
- 优先级：A
- 为什么重要：Hash table 是平均常数时间查找的核心结构，也承载 equals/hashCode 契约。
- 核心问题：如何把任意 key 映射到桶，并在 collision 和 resizing 下保持可用性能。
- 应该包含的内容：bucket、hashCode、mod、collision、load factor、resizing、HashSet contains 过程、mutable key 风险。
- 相关实现：HashSet、HashMap、Trie child map 改进。
- 相关课程连接：
  - CS61A：字典 / table。
  - CSAPP：哈希索引、内存定位。
  - Machine Learning：feature hashing、embedding lookup。
  - UMich DL：embedding table / indexing。
- 需要人工补充：collision handling 的标准策略可补充。

### [[heap]]

- 推荐文件名：heap.md
- 来源：CS61B
- 优先级：A
- 为什么重要：Heap 用很弱的局部 invariant 支撑高效极值访问，是 PQ、heap sort、Dijkstra、Prim 的基础。
- 核心问题：为什么不需要全局排序也能快速得到最小或最大元素。
- 应该包含的内容：complete binary tree、min-heap property、swim、sink、array-backed heap、parent/child index。
- 相关实现：Binary min-heap、heap sort、PriorityQueue。
- 相关课程连接：
  - CS61A：树结构。
  - CSAPP：数组布局。
  - Machine Learning：top-k、beam search 有连接。
  - UMich DL：top-k / priority scheduling 有弱连接。
- 需要人工补充：最大堆和最小堆对照可补充。

### [[priority-queue]]

- 推荐文件名：priority-queue.md
- 来源：CS61B
- 优先级：A
- 为什么重要：PriorityQueue 是从基础数据结构进入图算法的关键桥梁。
- 核心问题：如何高效支持 add、getSmallest、removeSmallest、decreasePriority。
- 应该包含的内容：MinPQ 操作、heap implementation、top-M 应用、Dijkstra 和 Prim 中的角色。
- 相关实现：Binary heap、Dijkstra、Prim、heap sort。
- 相关课程连接：
  - CS61A：抽象数据类型。
  - CSAPP：系统调度有弱连接。
  - Machine Learning：beam search、top-k。
  - UMich DL：search / sampling 中的 top-k。
- 需要人工补充：decreasePriority 的实现细节。

### [[union-find]]

- 推荐文件名：union-find.md
- 来源：CS61B
- 优先级：A
- 为什么重要：UnionFind 是动态连通性和 Kruskal MST 的核心，也展示了 weighted union 与 path compression 的威力。
- 核心问题：如何高效回答两个元素是否在同一集合中。
- 应该包含的内容：connect/union、isConnected、树表示、root、weighted quick union、path compression、近似常数复杂度。
- 相关实现：Disjoint Set、Kruskal cycle detection。
- 相关课程连接：
  - CS61A：集合抽象。
  - CSAPP：连接较弱。
  - Machine Learning：聚类连通分量有弱连接。
  - UMich DL：连接较弱。
- 需要人工补充：QuickFind / QuickUnion 对比可补充。

### [[graph]]

- 推荐文件名：graph.md
- 来源：CS61B
- 优先级：A
- 为什么重要：Graph 是 BFS、DFS、最短路径、MST、DAG、拓扑排序的统一模型。
- 核心问题：如何表示节点和边，并在表示选择下运行算法。
- 应该包含的内容：vertex、edge、simple graph、connected graph、adjacency matrix、edge set、adjacency list、`Theta(V + E)`。
- 相关实现：Graph adjacency list、DFS、BFS、Dijkstra、Prim、Kruskal、topological sort。
- 相关课程连接：
  - CS61A：递归搜索。
  - CSAPP：依赖图、控制流图有弱连接。
  - Machine Learning：图模型、computation graph。
  - UMich DL：computation graph。
- 需要人工补充：有向图/无向图 API 可补充。

### [[bfs]]

- 推荐文件名：bfs.md
- 来源：CS61B
- 优先级：A
- 为什么重要：BFS 是无权最短路径和层序搜索的基础算法。
- 核心问题：为什么队列逐层扩展能得到无权图的最短路径。
- 应该包含的内容：queue、visited、distTo、edgeTo、fringe、最大层宽空间成本、和 DFS 的区别。
- 相关实现：Graph traversal、unweighted shortest path。
- 相关课程连接：
  - CS61A：树/图搜索。
  - CSAPP：状态空间搜索有弱连接。
  - Machine Learning：搜索、图传播。
  - UMich DL：图/计算图遍历有弱连接。
- 需要人工补充：完整伪代码可补充。

### [[dfs]]

- 推荐文件名：dfs.md
- 来源：CS61B
- 优先级：A
- 为什么重要：DFS 是图可达性、路径恢复、拓扑排序和树遍历的基础。
- 核心问题：如何沿路径深入，并通过 marked 避免重复访问和环。
- 应该包含的内容：recursive stack、marked、edgeTo、preorder、postorder、回溯、拓扑排序中的后序反转。
- 相关实现：Graph DFS、tree traversal、topological sort。
- 相关课程连接：
  - CS61A：tree recursion、recursive search。
  - CSAPP：深度搜索状态空间有弱连接。
  - Machine Learning：图搜索有弱连接。
  - UMich DL：computation graph traversal 有弱连接。
- 需要人工补充：iterative DFS 可补充。

### [[complexity-analysis]]

- 推荐文件名：complexity-analysis.md
- 来源：CS61B
- 优先级：A
- 为什么重要：复杂度分析是选择数据结构和算法的共同语言。
- 核心问题：如何用增长阶评价实现策略，而不是依赖机器运行时间。
- 应该包含的内容：worst case、Theta、Big-O、Omega、忽略低阶项、amortized analysis、recursion tree、decision tree lower bound。
- 相关实现：resizing array、UnionFind、merge sort、quick sort、heap sort、hash table。
- 相关课程连接：
  - CS61A：递归过程复杂度。
  - CSAPP：性能分析、缓存和常数因子。
  - Machine Learning：训练复杂度、数据规模。
  - UMich DL：模型训练计算量。
- 需要人工补充：平均情况与概率分析可补充。

## 2. 中优先级概念 B

### [[equals]]

- 推荐文件名：equals.md
- 来源：CS61B
- 优先级：B
- 为什么重要：对象相等性影响集合、哈希表和 API 行为。
- 核心问题：何时两个对象应被视为相等，而不是仅仅地址相同。
- 应该包含的内容：默认 equals、`==` vs equals、重写 equals、和 hashCode 的关系。
- 相关实现：Object methods、HashSet contains。
- 相关课程连接：
  - CS61A：相等性与对象身份。
  - CSAPP：地址与值。
  - Machine Learning：数据对象去重有弱连接。
  - UMich DL：连接较弱。
- 需要人工补充：equals 的完整 Java contract 可补充。

### [[hashCode]]

- 推荐文件名：hashCode.md
- 来源：CS61B
- 优先级：B
- 为什么重要：hashCode 直接决定哈希容器能否找到对象。
- 核心问题：如何让相等对象进入一致的桶，并尽量均匀分布。
- 应该包含的内容：默认 hashCode、内容 hash、均匀分布、`equals` / `hashCode` contract、可变 key 风险。
- 相关实现：HashSet、HashMap。
- 相关课程连接：
  - CS61A：字典实现。
  - CSAPP：哈希定位、内存地址。
  - Machine Learning：feature hashing。
  - UMich DL：embedding / indexing。
- 需要人工补充：常见 hash function 设计可补充。

### [[static-type]]

- 推荐文件名：static-type.md
- 来源：CS61B
- 优先级：B
- 为什么重要：静态类型决定编译器允许调用哪些方法，是 Java OOP 和多态的基础。
- 核心问题：变量声明类型如何约束表达式和方法调用。
- 应该包含的内容：Java 静态类型、声明类型、接口类型参数、编译期检查。
- 相关实现：List61B 参数接收 AList、泛型容器。
- 相关课程连接：
  - CS61A：动态语言对比。
  - CSAPP：编译期信息。
  - Machine Learning：类型化 API 有弱连接。
  - UMich DL：连接较弱。
- 需要人工补充：dynamic type 对照需要补充。

### [[dynamic-type]]

- 推荐文件名：dynamic-type.md
- 来源：CS61B
- 优先级：B
- 为什么重要：动态类型解释了多态调用最终由实际对象实现响应。
- 核心问题：接口引用指向具体对象时，运行时调用哪个方法。
- 应该包含的内容：dynamic type、method dispatch、overriding、upcasting。
- 相关实现：List61B 引用指向 AList、overriding。
- 相关课程连接：
  - CS61A：对象运行时行为。
  - CSAPP：动态分派和运行时机制有连接。
  - Machine Learning：多模型统一接口。
  - UMich DL：Module 子类运行时 dispatch。
- 需要人工补充：index.md 标记 static type vs dynamic type 对照不足。

### [[overriding]]

- 推荐文件名：overriding.md
- 来源：CS61B
- 优先级：B
- 为什么重要：overriding 是多态和实现优化的机制。
- 核心问题：子类如何替换父类或接口默认方法的行为。
- 应该包含的内容：相同 signature、子类重写、default method override、和 overloading 的区别。
- 相关实现：List61B default method、equals 重写。
- 相关课程连接：
  - CS61A：方法覆盖。
  - CSAPP：动态分派有弱连接。
  - Machine Learning：模型方法覆盖。
  - UMich DL：forward 方法覆盖。
- 需要人工补充：override annotation 可补充。

### [[overloading]]

- 推荐文件名：overloading.md
- 来源：CS61B
- 优先级：B
- 为什么重要：overloading 容易和 overriding 混淆，也是 interface 抽象动机之一。
- 核心问题：同名方法如何通过参数列表区分。
- 应该包含的内容：方法名相同、参数列表不同、代码重复风险、用 interface 减少重复。
- 相关实现：L8 中洗澡方法例子、interface 重构动机。
- 相关课程连接：
  - CS61A：连接较弱。
  - CSAPP：编译期函数解析有弱连接。
  - Machine Learning：API overload 有弱连接。
  - UMich DL：连接较弱。
- 需要人工补充：Java overload resolution 细节可补充。

### [[comparable]]

- 推荐文件名：comparable.md
- 来源：CS61B
- 优先级：B
- 为什么重要：Comparable 让对象定义自然顺序，是排序、BST、泛型边界的基础。
- 核心问题：对象如何声明“我可以和同类比较大小”。
- 应该包含的内容：`compareTo`、natural ordering、`T extends Comparable<T>`、BST key 可比较。
- 相关实现：sorting、BST、generic max / compare。
- 相关课程连接：
  - CS61A：排序比较。
  - CSAPP：连接较弱。
  - Machine Learning：排序/排名有弱连接。
  - UMich DL：ranking 有弱连接。
- 需要人工补充：compareTo contract 可补充。

### [[comparator]]

- 推荐文件名：comparator.md
- 来源：CS61B
- 优先级：B
- 为什么重要：Comparator 允许外部定义比较规则，比 Comparable 更灵活。
- 核心问题：当对象可能有多种排序方式时，比较逻辑应放在哪里。
- 应该包含的内容：Comparator vs Comparable、外部比较器、排序策略。
- 相关实现：sorting、polymorphism examples。
- 相关课程连接：
  - CS61A：高阶比较函数。
  - CSAPP：连接较弱。
  - Machine Learning：ranking metric / custom ordering。
  - UMich DL：连接较弱。
- 需要人工补充：具体 Java Comparator 代码可补充。

### [[recursion-on-trees]]

- 推荐文件名：recursion-on-trees.md
- 来源：CS61B
- 优先级：B
- 为什么重要：树递归是遍历、BST 操作、DFS、递归复杂度分析的共同模式。
- 核心问题：如何把树问题拆成当前节点和子树问题。
- 应该包含的内容：preorder、inorder、postorder、base case、recursive traversal、recursion tree complexity。
- 相关实现：tree traversal、BST search/remove、merge sort recursion tree。
- 相关课程连接：
  - CS61A：tree recursion 核心连接。
  - CSAPP：递归栈。
  - Machine Learning：decision tree traversal。
  - UMich DL：computation graph traversal 有弱连接。
- 需要人工补充：现有笔记有遍历，但概念卡可补更多递归模板。

### [[graph-traversal]]

- 推荐文件名：graph-traversal.md
- 来源：CS61B
- 优先级：B
- 为什么重要：graph traversal 统一 BFS、DFS、路径恢复、拓扑排序。
- 核心问题：图允许环，遍历时如何避免重复访问并记录路径。
- 应该包含的内容：marked/visited、edgeTo、DFS stack、BFS queue、tree traversal vs graph traversal。
- 相关实现：DFS、BFS、topological sort。
- 相关课程连接：
  - CS61A：搜索。
  - CSAPP：控制流图遍历有弱连接。
  - Machine Learning：图传播。
  - UMich DL：computation graph traversal。
- 需要人工补充：可补统一伪代码。

### [[resizing-array]]

- 推荐文件名：resizing-array.md
- 来源：CS61B
- 优先级：B
- 为什么重要：resizing array 是摊还分析和工程性能权衡的直接案例。
- 核心问题：如何让固定长度数组表现得像可增长结构。
- 应该包含的内容：capacity、size、copy、加法扩容 vs 乘法扩容、amortized cost。
- 相关实现：AList、Hash table resizing。
- 相关课程连接：
  - CS61A：序列实现。
  - CSAPP：连续内存和复制成本。
  - Machine Learning：动态 buffer 有弱连接。
  - UMich DL：tensor resizing 通常不直接类比。
- 需要人工补充：缩容策略可补充。

### [[collision-handling]]

- 推荐文件名：collision-handling.md
- 来源：CS61B
- 优先级：B
- 为什么重要：collision 是哈希表从理想常数时间退化到线性时间的关键原因。
- 核心问题：多个 key 映射到同一桶时如何保持正确性和性能。
- 应该包含的内容：bucket、linked-list chaining、load factor、resizing、bad hashCode、equals 判断。
- 相关实现：HashSet、HashMap。
- 相关课程连接：
  - CS61A：dictionary collision。
  - CSAPP：hash indexing。
  - Machine Learning：feature hashing collision。
  - UMich DL：embedding hash collision 有弱连接。
- 需要人工补充：open addressing 等策略没有充分笔记依据。

## 3. 低优先级概念 C

- [[java-syntax]]
  - 推荐文件名：java-syntax.md
  - 为什么暂时是 C：它是必要背景，但不如 ADT、数据结构 invariant 和复杂度分析长期复用频率高。
  - 未来什么时候需要整理：复习 Java 基础语法、对象创建、数组和 Map 时。

- [[object-creation]]
  - 推荐文件名：object-creation.md
  - 为什么暂时是 C：内容较基础，可并入 Java/OOP 卡片。
  - 未来什么时候需要整理：需要系统复习 constructor、`new`、引用和值传递时。

- [[static-method]]
  - 推荐文件名：static-method.md
  - 为什么暂时是 C：是语言细节，适合放在 Java/OOP 或 static-type 卡片下。
  - 未来什么时候需要整理：复习 class-level method、static generic method 时。

- [[sentinel-node]]
  - 推荐文件名：sentinel-node.md
  - 为什么暂时是 C：很重要但可先作为 linked-list 的子概念。
  - 未来什么时候需要整理：整理 linked-list 边界条件模式时。

- [[b-tree]]
  - 推荐文件名：b-tree.md
  - 为什么暂时是 C：是平衡树扩展，当前主骨架先保证 BST、hash、heap、graph。
  - 未来什么时候需要整理：复习平衡树、2-3 tree、数据库索引时。

- [[llrb]]
  - 推荐文件名：llrb.md
  - 为什么暂时是 C：实现细节较深，依赖 BST、B-tree、tree rotation。
  - 未来什么时候需要整理：系统复习平衡 BST 或红黑树时。

- [[trie]]
  - 推荐文件名：trie.md
  - 为什么暂时是 C：字符串专用结构，重要但不影响当前核心骨架。
  - 未来什么时候需要整理：复习 prefix query、autocomplete、字符串 Map 时。

- [[dijkstra]]
  - 推荐文件名：dijkstra.md
  - 为什么暂时是 C：依赖 graph、priority-queue、relaxation，适合在图基础卡完成后整理。
  - 未来什么时候需要整理：复习带权最短路径时。

- [[minimum-spanning-tree]]
  - 推荐文件名：minimum-spanning-tree.md
  - 为什么暂时是 C：依赖 graph、priority-queue、union-find。
  - 未来什么时候需要整理：复习 Prim、Kruskal、cut property 时。

- [[topological-sort]]
  - 推荐文件名：topological-sort.md
  - 为什么暂时是 C：属于 DAG 专题，先不影响 BFS/DFS 主线。
  - 未来什么时候需要整理：复习依赖排序、DAG shortest path 时。

- [[radix-sort]]
  - 推荐文件名：radix-sort.md
  - 为什么暂时是 C：属于排序专题的扩展，不是当前概念骨架优先项。
  - 未来什么时候需要整理：复习非比较排序、LSD/MSD 时。

- [[stable-sort]]
  - 推荐文件名：stable-sort.md
  - 为什么暂时是 C：是排序性质，适合并入 sorting 或 radix-sort 卡片。
  - 未来什么时候需要整理：比较 Java 引用类型排序和基本类型排序时。

## 4. 推荐创建顺序

1. [[abstraction]]
2. [[ADT]]
3. [[interface]]
4. [[polymorphism]]
5. [[generics]]
6. [[linked-list]]
7. [[array-list]]
8. [[complexity-analysis]]
9. [[tree]]
10. [[binary-search-tree]]
11. [[hash-table]]
12. [[heap]]
13. [[priority-queue]]
14. [[union-find]]
15. [[graph]]

## 5. 跨课程连接候选

### [[recursion-on-trees]]

- 连接到 CS61A：tree recursion、recursive list/tree processing。
- 连接到 CSAPP：递归调用栈、函数调用成本。
- 连接到 Machine Learning：decision tree traversal、搜索空间。
- 连接到 UMich DL：computation graph traversal 有弱连接。
- 连接理由：CS61B 的 tree traversal、BST、DFS 都建立在递归拆分结构上。

### [[abstraction]]

- 连接到 CS61A：data abstraction、ADT。
- 连接到 CSAPP：硬件/系统接口隐藏底层实现。
- 连接到 Machine Learning：模型接口、训练流程封装。
- 连接到 UMich DL：layer/module 抽象。
- 连接理由：CS61B 用 SLList、AList、Graph 展示“使用者不依赖表示”的工程设计。

### [[linked-list]]

- 连接到 CS61A：recursive list、pair。
- 连接到 CSAPP：指针、堆内存、非连续内存布局。
- 连接到 Machine Learning：连接较弱。
- 连接到 UMich DL：连接较弱。
- 连接理由：链表是从抽象序列进入具体内存引用结构的第一批例子。

### [[array-list]]

- 连接到 CS61A：sequence abstraction。
- 连接到 CSAPP：连续内存、复制成本、缓存局部性。
- 连接到 Machine Learning：数组化数据、batch storage。
- 连接到 UMich DL：tensor storage 有远连接。
- 连接理由：AList 把逻辑长度、物理容量、扩容成本和内存布局连接起来。

### [[hash-table]]

- 连接到 CS61A：dictionary / table。
- 连接到 CSAPP：哈希索引、地址和内存定位。
- 连接到 Machine Learning：feature hashing、embedding lookup。
- 连接到 UMich DL：embedding table / indexing。
- 连接理由：hash table 是 indexing 和近似常数时间查找的长期概念。

### [[graph]]

- 连接到 CS61A：递归搜索、状态空间。
- 连接到 CSAPP：控制流图、依赖图有弱连接。
- 连接到 Machine Learning：图模型、搜索、传播。
- 连接到 UMich DL：computation graph。
- 连接理由：图是 CS61B 后半段算法统一模型，也能连接 ML/DL 的计算依赖关系。

### [[bfs]]

- 连接到 CS61A：搜索、层序遍历。
- 连接到 CSAPP：状态空间搜索有弱连接。
- 连接到 Machine Learning：图传播、最短步数搜索。
- 连接到 UMich DL：计算图层级遍历有弱连接。
- 连接理由：BFS 的层次扩展解释了无权最短路径和 queue-based traversal。

### [[dfs]]

- 连接到 CS61A：递归搜索、tree recursion。
- 连接到 CSAPP：递归栈和状态探索有弱连接。
- 连接到 Machine Learning：图搜索、依赖遍历。
- 连接到 UMich DL：computation graph traversal。
- 连接理由：DFS 连接递归、marked 状态、回溯、拓扑排序。

### [[complexity-analysis]]

- 连接到 CS61A：递归过程增长阶。
- 连接到 CSAPP：性能分析、常数因子、内存层级影响。
- 连接到 Machine Learning：训练时间、数据规模、算法选择。
- 连接到 UMich DL：模型计算量、训练成本。
- 连接理由：复杂度分析是跨课程讨论效率和可扩展性的共同语言。

## 6. 不要做的事

- 不要创建具体 concept 文件。
- 不要生成 mistakes。
- 不要修改任何原始笔记。
- 不要逐文件总结。
- 不要编造 index.md 或笔记中没有依据的内容。
- 不要把 TODO 写成普通目录清单。
- 不要输出空泛套话。
