---
title: 有向图的连通性
math: true
date: 2022-05-27 11:24:31
categories: 课程笔记
tags: 离散数学
index_img:
banner_img:
---

设有向图$D=<V,E>$

+ **u可达v $(u\rightarrow v)$**：u 到 v 有一条有向路径。

+ <u>规定 u 到自身总是可达的。</u>

+ **互相可达 $(u\iff v)$**：$u\rightarrow v 且 v\rightarrow u$。

+ ==可达== 具有自反性和传递性，但不一定具有对称性。

+ **u 到 v 的距离(或短程线）：**u 到 v长度具有最短的路径长度(u 可达 v)，记作 $d<u,v>$。

+ 规定：若 u 不可达 v，$d<u,v> = \infty$。

+ **距离的性质：**

  $\begin{aligned}&d<u,v>\geq0\\&d<u,u> = 0\\&d<u,v> + d<v,w> \geq d<u,w>\\&d<u,v> \neq d<v,u>\end{aligned}$

![c0aJIO.png](https://z3.ax1x.com/2021/04/11/c0aJIO.png)



图的直径：$D = max_{u,v\in V}d<u,v>$

**弱连通的**：有向图 D 的 ==基图== 是连连通的。（<u>有向图的基图是无向图</u>）

**单向连通的**（单侧连通）：$\exist u,v\in V(D),使得 u\rightarrow v,v\rightarrow u$，即有向图中存在两点互相可达。

**强连通的**：$\forall u,v\in V(D),使得 u\rightarrow v,v\rightarrow u$，即有向图中任意两点互相可达。

> 结论：
>
> + 强连通图一定是单项连通的
> + 单项连通图一定是弱连通的

😑**强连通图、单项连通图判定定理**

+ 强连通$\iff$图中存在一条**回路**，经过每个顶点至少一次。
+ 单项连通$\iff$图中存在一条**通路**，经过每个顶点至少一次。

在简单有向图中：

+ **强分图：**具有 ==强连通性质== 的极大子图
+ **单向分图**：具有 ==单向连通性质== 的极大子图
+ **弱分图**：具有 ==弱连通性质== 的极大子图

+ **定理**：在有向图$D=<V,E>$中，他的每一个顶点位于且仅位于一个强分图中。


