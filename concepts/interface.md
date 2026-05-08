---
type: concept
course: CS61B
priority: A
status: draft
aliases: []
related:
  - "[[abstraction]]"
  - "[[adt]]"
  - "[[polymorphism]]"
  - "[[generics]]"
  - "[[linked-list]]"
  - "[[array-list]]"
---

# Interface

## 一句话定义

[[interface]] 是 Java 中表达“某类对象必须支持哪些操作”的类型机制。它在 CS61B 中解决的问题是：让客户端代码依赖行为标准，而不是依赖某个具体实现类。

## 核心思想

interface 把“能做什么”从“怎么做”中抽出来。L8 中 List61B 的例子说明，方法参数可以写成接口类型，从而接收 AList 等具体实现；只要类实现了接口要求的方法，它就能被当作这个抽象类型使用。

这让重复的 overloaded 方法可以收敛成面向共同类型的一套逻辑，也让实现类可以在必要时 override 默认方法。interface 本身不是对象，不能直接实例化；它更像客户端和实现之间的标准。

## 核心边界 / Contract / Invariant

client 能依赖 interface 中声明的公开方法，以及这些方法承诺的行为。implementation 隐藏的是字段、节点结构、数组布局、缓存策略和优化细节。

interface 的 contract 是：实现类必须提供接口要求的方法，并保证这些方法满足语义约束。无单一固定 invariant，重点在于抽象边界和使用约束；具体 invariant 由实现类维护，例如 SLList 的链表结构或 AList 的数组容量。

## 在 CS61B 中的位置

[[abstraction]] 和 [[adt|ADT]] 说明为什么要分离行为与表示，[[interface]] 则是 Java 中实现这种分离的主要工具。它进一步连接 [[polymorphism]]、[[generics]]、Comparable / Comparator，以及后续 Set、Map、PriorityQueue 这类可替换实现。

## 典型实现

- List61B：解决 SLList、AList 等 List 实现共享客户端代码的问题；核心思想是把列表操作声明为接口；相关概念：[[ADT]]、[[linked-list]]、[[array-list]]。
- Set61B：解决集合类共享标准的问题；核心思想是接口也可以继承接口；相关概念：[[2. Scope, Static, Linked Lists, Arrays/L8 Interface and Implementation Inheritance/L8 Interface and Implementation Inheritance|inheritance]]、[[3. DataStructure and Algorithm/L16 Extends, Sets, Maps, and BSTs/L16 Extends, Sets, Maps, and BSTs|set]]。
- Comparable：解决对象声明自然顺序的问题；核心思想是实现 `compareTo` contract；相关概念：[[2. Scope, Static, Linked Lists, Arrays/L9 Subtype Polymorphism, Comparators, Comparables, Generic Functions/L9 Subtype Polymorphism, Comparators, Comparables, Generic Functions|comparable]]、[[generics]]。
- Comparator：解决外部比较规则的问题；核心思想是把比较策略放到独立对象中；相关概念：[[2. Scope, Static, Linked Lists, Arrays/L9 Subtype Polymorphism, Comparators, Comparables, Generic Functions/L9 Subtype Polymorphism, Comparators, Comparables, Generic Functions|comparator]]、[[polymorphism]]。

## 容易混淆点

- interface vs implementation：interface 规定能调用什么，implementation 决定怎么完成。
- interface vs class：interface 不能直接实例化，class 可以创建对象。
- overloading vs interface 参数：overloading 为不同参数写多个方法，interface 让共同类型共享一套方法。
- default method vs overriding：default method 给默认行为，具体类仍可重写优化。
- interface inheritance vs implementation inheritance：前者继承操作标准，后者复用具体代码。

## 相关概念

- [[abstraction]]
- [[adt|ADT]]
- [[polymorphism]]
- [[2. Scope, Static, Linked Lists, Arrays/L8 Interface and Implementation Inheritance/L8 Interface and Implementation Inheritance|inheritance]]
- [[2. Scope, Static, Linked Lists, Arrays/L8 Interface and Implementation Inheritance/L8 Interface and Implementation Inheritance|overriding]]
- [[2. Scope, Static, Linked Lists, Arrays/L9 Subtype Polymorphism, Comparators, Comparables, Generic Functions/L9 Subtype Polymorphism, Comparators, Comparables, Generic Functions|comparable]]
- [[2. Scope, Static, Linked Lists, Arrays/L9 Subtype Polymorphism, Comparators, Comparables, Generic Functions/L9 Subtype Polymorphism, Comparators, Comparables, Generic Functions|comparator]]

## 跨课程连接

- CS61A：连接数据抽象和通用函数接口。
- CSAPP：可连接模块边界与调用契约，但需要人工补充具体例子。
- Machine Learning：统一模型 API 让不同模型共享 train / predict 形式。
- UMich DL：layer / module API 让不同层共享 forward 调用边界。
