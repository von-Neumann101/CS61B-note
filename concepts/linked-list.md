---
type: concept
course: CS61B
priority: A
status: draft
aliases: []
related:
  - "[[abstraction]]"
  - "[[adt]]"
  - "[[array-list]]"
  - "[[tree]]"
  - "[[complexity-analysis]]"
---

# Linked List

## 一句话定义

[[linked-list]] 是用节点和引用表示线性序列的数据结构。它在 CS61B 中解决的问题是：不用连续数组也能增长序列，并借助抽象屏障隐藏节点操作。

## 核心思想

IntList 暴露了递归节点结构，用户需要直接构造 `new IntList(x, rest)`，这没有形成稳定接口。SLList 把节点封装到列表类内部，用 `addFirst`、`getFirst`、`addLast` 等方法让客户端只操作 List，而不是操作 `IntNode`。

链表的工程重点在于引用结构的维护。单向链表只知道 next，维护 last 可以让访问末尾更快，但删除末尾仍找不到前驱；双向链表给节点增加 prev，让节点能向前后两个方向移动。sentinel node 和 size 缓存则用额外状态减少特殊分支和重复遍历。

## 核心边界 / Contract / Invariant

核心 invariant 是：每个节点保存一个 item 和指向相邻节点的引用；列表对象保存进入结构的入口，例如 `first`、`last` 或 sentinel；`size` 如果被缓存，就必须与实际节点数一致。双向链表还要求 `next.prev` 和 `prev.next` 互相匹配。

这个 invariant 保证遍历不会丢节点，头尾操作能找到正确位置，size 查询可信。如果引用断开、形成错误环、prev/next 不一致或 size 没同步，结果可能是元素丢失、无限遍历、删除错误节点或复杂度判断失真。

## 在 CS61B 中的位置

[[linked-list]] 是从引用类型进入数据结构实现的第一批核心例子。它连接 [[abstraction]]、[[adt|ADT]]、[[1. Introduction to Java/L4 SLList/L4 SLList|sentinel-node]] 和后续 List 实现对比，也为 tree、graph 这类引用结构打基础。

## 典型实现

- IntList：解决可扩展整数序列的问题；核心思想是递归节点 `item/rest`；相关概念：[[1. Introduction to Java/L3 Reference Recursion intList/L3 Reference Recursion intList|reference-type]]、[[1. Introduction to Java/L3 Reference Recursion intList/L3 Reference Recursion intList|recursion]]。
- SLList / IntNode：解决裸节点暴露的问题；核心思想是列表类封装 `first` 和节点操作；相关概念：[[1. Introduction to Java/L4 SLList/L4 SLList|abstraction-barrier]]、[[1. Introduction to Java/L4 SLList/L4 SLList|private]]。
- Sentinel SLList：解决空表和非空表特殊分支的问题；核心思想是用哨兵统一入口；相关概念：[[1. Introduction to Java/L4 SLList/L4 SLList|sentinel-node]]、invariant。
- DLList：解决单向链表难以前向访问的问题；核心思想是每个节点保存 `prev` 和 `next`；相关概念：[[1. Introduction to Java/L5 List/L5 List|doubly-linked-list]]。

## 容易混淆点

- IntList vs SLList：前者暴露递归节点，后者用类封装操作。
- SLList vs DLList：前者只有 next，后者同时维护 prev / next。
- sentinel vs null special case：sentinel 用统一节点模型减少空表分支。
- maintaining last vs deleting last：有 last 能快速找到尾节点，但单向链表仍找不到前驱。
- linked list vs array list：链表节点不连续，数组列表依赖连续存储和 resizing。

## 相关概念

- [[1. Introduction to Java/L3 Reference Recursion intList/L3 Reference Recursion intList|intlist]]
- [[1. Introduction to Java/L4 SLList/L4 SLList|sllist]]
- [[1. Introduction to Java/L5 List/L5 List|doubly-linked-list]]
- [[1. Introduction to Java/L4 SLList/L4 SLList|sentinel-node]]
- [[1. Introduction to Java/L4 SLList/L4 SLList|abstraction-barrier]]
- [[array-list]]

## 跨课程连接

- CS61A：连接 recursive list、pair/list 和递归处理。
- CSAPP：连接指针、引用、非连续内存布局。
- Machine Learning：连接较弱，需要人工补充。
- UMich DL：连接较弱，需要人工补充。
