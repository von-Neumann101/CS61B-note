---
type: concept
course: CS61B
priority: A
status: draft
aliases: []
related:
  - "[[interface]]"
  - "[[polymorphism]]"
  - "[[adt]]"
  - "[[binary-search-tree]]"
  - "[[priority-queue]]"
---

# Generics

## 一句话定义

[[generics]] 是 Java 中用类型参数写类或方法的机制，让数据结构和算法可以在多种元素类型上安全工作。它在 CS61B 中解决的问题是：List、Map、比较函数等不应只服务 `int` 或某个具体类。

## 核心思想

泛型把“元素是什么类型”变成参数。这样 List 可以是 `List<String>` 或 `List<Integer>`，随机选择函数也可以从任意类型数组中取元素。L9 笔记中特别区分了类的泛型参数和 `static` 方法：静态方法不属于对象维度，因此需要声明自己的方法级类型参数。

泛型还可以加边界。比如当算法需要比较元素时，不能只写任意 `T`，而要说明 `T extends Comparable<T>`，这样编译器才知道 `compareTo` 可用。

## 核心边界 / Contract / Invariant

compile-time 边界是：类型参数限制了能放入和取出的元素类型，也限制了能调用的方法。runtime 行为仍由实际对象和多态决定；泛型本身不替代 interface，而是经常和 interface 一起表达“任意 T，但 T 必须满足某个 contract”。

泛型的 contract 是：代码不能假设 `T` 有未声明的能力。无单一固定 invariant，重点在于抽象边界和使用约束；如果需要排序或比较，必须通过 Comparable、Comparator 或 bounded type parameter 明确写出。

## 在 CS61B 中的位置

[[interface]] 和 [[polymorphism]] 解决“不同实现类共享行为”，[[generics]] 解决“同一结构支持不同元素类型”。它让 List、Map、Set、PriorityQueue 和比较算法摆脱具体类型，并把类型错误尽量提前到编译期。

## 典型实现

- Generic List / Map：解决容器只能存单一固定类型的问题；核心思想是用类型参数表示元素或 key/value；相关概念：[[ADT]]、[[interface]]。
- Generic static method：解决静态方法不能直接使用类级泛型参数的问题；核心思想是在方法签名中声明 `<T>`；相关概念：[[2. Scope, Static, Linked Lists, Arrays/L9 Subtype Polymorphism, Comparators, Comparables, Generic Functions/L9 Subtype Polymorphism, Comparators, Comparables, Generic Functions|static-method]]。
- `T extends Comparable<T>`：解决泛型算法需要比较元素的问题；核心思想是用 bounded type parameter 暴露 `compareTo`；相关概念：[[2. Scope, Static, Linked Lists, Arrays/L9 Subtype Polymorphism, Comparators, Comparables, Generic Functions/L9 Subtype Polymorphism, Comparators, Comparables, Generic Functions|comparable]]、[[polymorphism]]。
- Comparator-based comparison：解决对象有多种比较方式的问题；核心思想是把比较规则作为外部对象传入；相关概念：[[2. Scope, Static, Linked Lists, Arrays/L9 Subtype Polymorphism, Comparators, Comparables, Generic Functions/L9 Subtype Polymorphism, Comparators, Comparables, Generic Functions|comparator]]。

## 容易混淆点

- generic class vs generic method：类级类型参数属于对象或类定义，静态方法需要自己的类型参数。
- generic type vs interface bound：`T` 只是未知类型，`T extends Comparable<T>` 才承诺可比较。
- generics vs polymorphism：泛型抽象元素类型，多态抽象具体实现行为。
- Comparable vs Comparator：一个把顺序放进类，一个把顺序放在外部策略。
- diamond syntax vs 类型推断细节：当前笔记依据有限，需要人工补充。

## 相关概念

- [[interface]]
- [[polymorphism]]
- [[2. Scope, Static, Linked Lists, Arrays/L9 Subtype Polymorphism, Comparators, Comparables, Generic Functions/L9 Subtype Polymorphism, Comparators, Comparables, Generic Functions|comparable]]
- [[2. Scope, Static, Linked Lists, Arrays/L9 Subtype Polymorphism, Comparators, Comparables, Generic Functions/L9 Subtype Polymorphism, Comparators, Comparables, Generic Functions|comparator]]
- [[2. Scope, Static, Linked Lists, Arrays/L9 Subtype Polymorphism, Comparators, Comparables, Generic Functions/L9 Subtype Polymorphism, Comparators, Comparables, Generic Functions|static-method]]
- [[adt|ADT]]

## 跨课程连接

- CS61A：连接通用数据结构和高阶抽象。
- CSAPP：类型系统连接较弱，需要人工补充。
- Machine Learning：可连接通用数据管线和模型 API，但当前笔记依据不足。
- UMich DL：可连接泛化 API 设计，但需要人工补充具体例子。
