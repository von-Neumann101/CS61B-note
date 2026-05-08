---
type: concept
course: CS61B
priority: A
status: draft
aliases: []
related:
  - "[[interface]]"
  - "[[generics]]"
  - "[[adt]]"
  - "[[abstraction]]"
---

# Polymorphism

## 一句话定义

[[polymorphism]] 是同一段客户端代码通过共同类型处理不同具体对象，并在运行时使用对象自己的实现。它在 CS61B 中解决的问题是：算法和数据结构客户端不必为 AList、SLList 或不同可比较对象各写一份逻辑。

## 核心思想

多态依赖抽象类型和具体实现分离。变量、参数或返回值可以声明为 interface 类型；实际传入的对象可以是任何实现该接口的类。L8 的 List61B 例子体现了向上转型：参数要求 List61B 时，AList 可以作为 List61B 使用。

这种设计让“同一个函数作用在不同对象上”成为可能。L9 中 Comparable / Comparator 的比较例子说明，只要对象满足比较接口，泛型算法就能调用比较操作，而不需要知道对象内部字段。

## 核心边界 / Contract / Invariant

static type 决定编译期能调用哪些方法；dynamic type 决定运行时具体执行哪个 overridden 方法。client 只能调用静态类型暴露的操作，不能假设对象一定是某个实现类，除非显式检查或转换。

多态的 contract 是：子类型必须能作为父类型或接口使用，并保持接口方法的语义。无单一固定 invariant，重点在于抽象边界和使用约束；具体 invariant 仍由动态类型对应的实现类维护。

## 在 CS61B 中的位置

[[interface]] 提供共同类型，[[polymorphism]] 让共同类型真正服务客户端复用。它连接 List61B 参数、Comparable / Comparator、generic functions，也解释了为什么 CS61B 后续更强调面向 ADT 写代码，而不是面向单个 class 写代码。

## 典型实现

- List61B 参数接收 AList：解决客户端代码绑定具体类的问题；核心思想是向上转型到接口类型；相关概念：[[interface]]、[[2. Scope, Static, Linked Lists, Arrays/L8 Interface and Implementation Inheritance/L8 Interface and Implementation Inheritance|upcasting]]。
- overriding：解决子类或实现类替换默认行为的问题；核心思想是相同 signature 在动态类型中执行具体版本；相关概念：[[2. Scope, Static, Linked Lists, Arrays/L8 Interface and Implementation Inheritance/L8 Interface and Implementation Inheritance|overriding]]、[[2. Scope, Static, Linked Lists, Arrays/L8 Interface and Implementation Inheritance/L8 Interface and Implementation Inheritance|inheritance]]。
- Comparable / Comparator：解决统一比较的问题；核心思想是算法依赖比较接口，不依赖对象内部表示；相关概念：[[2. Scope, Static, Linked Lists, Arrays/L9 Subtype Polymorphism, Comparators, Comparables, Generic Functions/L9 Subtype Polymorphism, Comparators, Comparables, Generic Functions|comparable]]、[[2. Scope, Static, Linked Lists, Arrays/L9 Subtype Polymorphism, Comparators, Comparables, Generic Functions/L9 Subtype Polymorphism, Comparators, Comparables, Generic Functions|comparator]]、[[generics]]。

## 容易混淆点

- static type vs dynamic type：前者限制能调用什么，后者影响实际执行什么。
- overloading vs overriding：overloading 是参数列表不同，overriding 是子类型重写相同 signature。
- interface parameter vs concrete parameter：前者允许多种实现，后者把代码绑定到单个类。
- subtype polymorphism vs generics：多态处理不同实现类，泛型处理不同元素类型。
- Comparable vs Comparator：前者是对象自身顺序，后者是外部比较规则。

## 相关概念

- [[interface]]
- [[2. Scope, Static, Linked Lists, Arrays/L8 Interface and Implementation Inheritance/L8 Interface and Implementation Inheritance|inheritance]]
- [[2. Scope, Static, Linked Lists, Arrays/L8 Interface and Implementation Inheritance/L8 Interface and Implementation Inheritance|upcasting]]
- [[2. Scope, Static, Linked Lists, Arrays/L8 Interface and Implementation Inheritance/L8 Interface and Implementation Inheritance|overriding]]
- [[generics]]
- [[2. Scope, Static, Linked Lists, Arrays/L9 Subtype Polymorphism, Comparators, Comparables, Generic Functions/L9 Subtype Polymorphism, Comparators, Comparables, Generic Functions|comparable]]
- [[2. Scope, Static, Linked Lists, Arrays/L9 Subtype Polymorphism, Comparators, Comparables, Generic Functions/L9 Subtype Polymorphism, Comparators, Comparables, Generic Functions|comparator]]

## 跨课程连接

- CS61A：连接通用函数和数据导向编程。
- CSAPP：可连接动态分派的运行时机制，但当前笔记依据不足，需要人工补充。
- Machine Learning：不同模型共享 predict / train 接口时依赖同类思想。
- UMich DL：不同 layer / module 子类共享 forward 调用方式。
