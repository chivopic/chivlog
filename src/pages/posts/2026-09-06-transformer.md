---
layout: ../../layouts/PostLayout.astro
title: "Transformer：终于理解了它在做什么"
description: "把 Transformer 先理解成：让每个词动态决定该关注序列里的哪些其他词。"
date: 2026-09-06
type: learned
source: https://arxiv.org/abs/1706.03762
note: "Transformer 的核心直觉终于顺了：每个 token 都会通过 attention 去判断当前最该关注谁，再逐层整合上下文。"
categories:
  - inbox
  - ai
  - learning
---

Transformer 最值得先记住的，不是一堆矩阵公式，而是一个直觉：

> **一句话里的每个 token，都可以动态决定自己应该关注其他哪些 token。**

这件事主要由 **Attention** 完成。

## 一个简单例子

比如：

> 小明把书给了小王，因为他已经看完了。

当模型处理“他”时，它需要结合上下文判断“他”更可能指谁。

Transformer 不只是从左到右机械地传递信息，而是让当前位置去观察整段上下文，并给不同位置分配不同的重要程度。

## Q、K、V 可以先这样理解

- **Query**：我现在想找什么信息？
- **Key**：我这里有什么信息可供匹配？
- **Value**：如果你关注我，我真正提供给你的内容是什么？

Query 和 Key 决定“关注谁”，然后把对应的 Value 聚合起来。

所以 Attention 可以粗略理解成：

```text
当前 token
   ↓
拿着 Query 去看其他 token 的 Key
   ↓
算出关注程度
   ↓
按权重汇总它们的 Value
   ↓
得到带上下文的新表示
```

## Multi-Head Attention

一个 attention head 可能关注语法关系，另一个可能关注指代、位置或语义关联。

Multi-Head Attention 就像同时从多个角度观察一句话，最后再把这些结果组合起来。

## 为什么 Transformer 重要

它让模型非常擅长处理长距离依赖，而且训练时可以大规模并行计算。

后来的 GPT、BERT，以及今天大量大语言模型，都建立在这套基本结构之上。

## 现在最值得继续深入的路线

```text
Attention 直觉
→ Q / K / V
→ scaled dot-product attention
→ multi-head attention
→ positional encoding
→ Transformer block
→ GPT 的 decoder-only 架构
→ LLM 如何生成下一个 token
```

先把 Attention 真正理解，再继续往后走，会比一开始直接啃完整 Transformer 结构容易很多。
