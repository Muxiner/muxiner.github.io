---
title: 图的矩阵表示
math: true
date: 2022-05-27 11:22:16
categories: 课程笔记
tags: 离散数学
index_img:
banner_img:
---

#### 10.1 关联矩阵

+ 有向图的**关联矩阵**：

  设 $D = <V,E>$是无环有向图，$V=\{V_1,V_2,...,V_n\}，E=\{e_1,e_2,...,e_m\}$，令
  $$
  m_{ij} = 
  \begin{cases}
  1,  \quad & v_i \text{是}e_j\text{的始点},\\
  0,  \quad & v_i \text{与}e_j\text{不关联}, \\
  -1, \quad & v_i \text{是}e_j\text{的终点},
  \end{cases}
  $$
  称 $[m_{{ij}_{m \times n}}]$ 为 D 的 <font color = red>关联矩阵</font>，记作 $M(D)$.

  $$
  M(D) = 
  
  \begin{bmatrix}
  -1&-1&1&0&0&0\\
  1&1&0&0&0&0\\
  0&0&-1&-1&1&-1\\
  0&0&0&0&-1&1
  \end{bmatrix}
  $$

  > 1. D每列元素之和 = 0 $\Longrightarrow \sum_{i = 1}^nm_{ij} = 0$，说明D中每条边关联两个顶点，一个始点，一个终点 
  > 2. 第$i$行元素绝对值之和 = $d(v_i)$，即$\sum_{j=1}^m|m_{ij}| = d(v_i)$，其中 1 的个数 等于 出度；-1 的个数等于入度
  > 3. $\sum_{i = 1}^n\sum_{j =1}^mm_{ij} = 0$，即出度入度相等 = m，符合握手定理
  > 4. 若$M(D)$中两列相同$\Longrightarrow$对应 的边是平行边

+ 无向图的**关联矩阵**：

  设 $G = <V,E>$是无环有向图，$V=\{V_1,V_2,...,V_n\}，E=\{e_1,e_2,...,e_m\}$，令
  $$
  m_{ij} = 
  \begin{cases}
  1,  \quad & v_i \text{是}e_j\text{关联},\\
  0,  \quad & v_i \text{与}e_j\text{不关联}, \\
  
  \end{cases}
  $$
  称 $[m_{{ij}_{m \times n}}]$ 为 G 的 <font color = red>关联矩阵</font>，记作 $M(G)$.

 
  > 1. $M(G)$中每列元素之和 = 2$\Longrightarrow\sum_{i=1}^nm_{ij}=2$，说明G中每条边有唯一的两个端点
  >
  > 2. $M(G)$中第$i$行中 1 个数 = $\sum_{j =1}^m = d(v_i)$
  >
  > 3. $M(G)中$第$i$行中1对应的边组成的集合为$v_i$的关联集，其为G中一个断集，当$v_i$不是割点时，其为扇形割集
  >
  > 4. $M(G)$中若两列相同，则它们对应的边是平行边
  >
  > 5. 若G有$k(k\geq2)$个连通分支，则G的关联矩阵$M(G)$有如下形式:
  >    $$
  >    M(G) = 
  >    \begin{bmatrix}
  >    M(G_1)\\
  >    &M(G_2)\\
  >    &&\ddots&\\
  >    &&&M(G_k)
  >    \end{bmatrix}
  >    $$
  >    其中$M(G_r)$是G中第 r 个联通分支的关联矩阵.

+ **基本关联矩阵：**

  G的**基本关联矩阵**是有$M(G)$删除任意一行所得的矩阵，被删除行对应的顶点是**参考点**

+ **定理 10.1：**

  n 阶无向连通图 G 的关联矩阵的秩 $r(M(G)) = n - 1$.

+ **定理 10.2：**

  n 阶无向连通图 G 的基本关联矩阵的秩 $r(M_f(G)) = n - 1$.

  推论：

  + 设n阶无向图G有p个连通分支，则$r(M(G)) = r(M_f(G)) = n - p$，其中$M_f(G)$是从$M(G)$的每个对角块中删除任意一行得到的矩阵。
  + G是连通图 $\iff$ $r(M(G)) = r(M_f(G)) = n - 1$

+ **定理 10.3：**

  设

  + $M_f(G)$是 n 阶连通图 G 的一个基本关联矩阵
  + $M_f'$是$M_f(G)$中任意 $n-1$列组成的方阵

  则

  $M_f'$中各列所对应的边集$\{e_{i_1},e_{i_2},...,e_{i_{n-1}}\}$的导出子图 $G[\{e_{i_1},e_{i_2},...,e_{i_{n-1}}\}]$是 G 的生成树$\iff M_f'$的行列式 $|M_f'| \neq 0$.



#### 10.2 邻接矩阵与相邻矩阵

+ **邻接矩阵：**

  n阶标定 ==有向图== D 中，$V(D)=\{v_1,v_2,...,v_n\}$，令$a_{ij}^{(1)}$为$v_1$邻接到$v_j$的边的条数。

  $[a_{ij}^{(1)}]_{n\times m}$是$D$的**邻接矩阵**，记作$A(D)$，简记 $A$。


  性质：

  + 第$i$行元素之和 = $v_i$的出度。

    A 中所有元素之和 = 各顶点出度之和 = 边数（m）

  + 第$j$列元素之和 = $v_j$的入度

    A 中所有元素之和 = 各顶点入度之和 = 边数 (m)

+ **定理 10.4**

  设 A 是 n 阶有向标定图的邻接矩阵，A 的$l(l\geq 2)$次幂$A^l = A^{l-1}$.

  + A 中元素 $a_{ij}^{(l)}$为$v_i$到$v_j$长度为$l$的**通路数**
  + $\sum_i\sum_ja_{ij}^{(l)}$ 是 D 中长度为 $l$ 的**通路总数**
  + $\sum_ia_{ii}^{(l)}$ 是 D 中长度为 $l$ 的**回路总数**

  推论：

  + 设 A 是 n 阶有向标定图的邻接矩阵，
    + $B^r$ 中元素 $b_{ij}^{(r)}$ 为 $v_i$ 到 $v_j$ 长度 $\leq r$ 的**通路数**
    + $\sum_i\sum_jb_{ij}^{(r)}$ 是 D 中长度 $\leq r$ 的**通路总数**
    + $\sum_ib_{ii}^{(r)}$ 是 D 中长度 $\leq r$ 的 **回路数**

  > 对角线上的$b_{ii}^{(r)}$、$A_{ii}^{(l)}$ 是回路数

+ **可达矩阵：**

  设 n 阶有向图 D 中， $V(D)=\{v_1,v_2,...,v_n\}$.
  $$
  p_{ij}=\begin{cases}
  1, \quad v_i\text{可达}v_j,\\
  0, \quad v_j\text{不可达}v_j
  \end{cases}
  $$
  称 $[p_{ij}]_{n\times m}$ 是 D 的**可达矩阵**，记作 $P(D)$，简记 $P$.

  性质：

  1. $\because \forall v_i \in V(D),v_i\text{可达}v_j, \therefore p \text{的主对角线元素全是} 1$.

  2. 若 D 是强连通的，则 P 的全体元素均为 1.

  3. 设 D 是具有$k(k\geq 2)$个连通分支$D_1,D_2,...,D_k$的有向图，$D_i = D[\{v_{i_1},v_{i_2},...,v_{m_i}\}], i = 1,2,...,k$，则
     $$
     P(D) = 
     \begin{bmatrix}
     P(D_1)\\
     &P(D_2)\\
     &&P(D_3)\\
     &&&\ddots\\
     &&&&P(D_K)\\
     \end{bmatrix}
     $$
     其中 $P(D_i)$ 是 $D_i$ 的可达矩阵。

  $\forall v_i,v_j\in V(D)\text{且}v_i\neq v_j,\therefore p_{ij} = 1\text{当且仅当}\quad b_{ij}^{(n-1)\neq 0}$.

+ **相邻矩阵：**

  设 n 阶 ==无向简单图== G 中，$V(G)=\{v_1,v_2,...,v_m\},\quad\text{令}a_{ij}^{(1)}=0,i=1,2,...,n,$
  $$
  a_{ij}^{(1)}=\begin{cases}
  1,\quad v_i\text{与}v_j\text{相邻}，i\neq j,\\
  0,\quad v_i\text{与}v_j\text{不相邻}，i = j,
  \end{cases}
  $$
  称 $[a_{ij}^{(1)}]_{n\times m}$ 是 G 的 **相邻矩阵**，记作$A(G)$，简记 $A$.



  性质：

  1. A 是 对称的
  2. $\sum_ja_{ij}^{(1)} = d(v_1)$
  3. $\sum_i\sum_ja_{ij}^{(1)} = \sum_id(v_i) = 2m,\text{其中}m\text{是边数,也是G中长度为1的通路数}$

+ 设 $A^k = A^{k-1}\bullet A = [a_{ij}^{k},\quad k = 2,3,...]$

  定理 10.5:

  设 n 阶 无相简单图 G 中，$V(D)=\{v_1,v_2,...,v_m\}$，A 是 G 的相邻矩阵.

  + $A^k$ 中元素 $a_{ij}^{(k)}(=a_{ji}^{(k)})(i \neq j)$ 是 $v_i$到 $v_j(v_j\text{到}v_i)$长度为k 的 **通路数**。
  + $a_{ii}^{(k)}$ 是 $v_i$ 到  $v_i$长度为k的**回路数**

  推论：

  1. $\text{在}A^2\text{中}，a_{ii}^{(2)}=d(v_i)$
  2. ？若G是连通图，对于$i\neq j,v_i,v_j$之间的距离$d(v_i,v_j)$ = 使$A^k$中元素$a_{ij}^{(k)}\neq 0$的最小正整数 k.

+ **连通矩阵：**

  设 n 阶 无相简单图 G 中，$V(D)=\{v_1,v_2,...,v_m\}$，令
  $$
  p_{ij}=\begin{cases}
  1,\quad v_i 与 v_j 连通，\\
  0,\quad v_i 与 v_j 不连通，
  \end{cases}
  $$
  称 $[p_{ij}]_{n\times m}$ 是 G 的连通图，记作$P(G)$，简记 $P$.

  性质：

  1. P 的主对角线元素均是 1

  2. 若 G 是连通图，则 P 中元素全是 1

  3. 设 G 是具有$k(k\geq 2)$个连通分支$G_1,G_2,...,G_k$的有向图，$G_i = G[\{v_{i_1},v_{i_2},...,v_{m_i}\}], i = 1,2,...,k$，则
     $$
     P(G) = \begin{bmatrix}
     P(G_1)\\
     &P(G_2)\\
     &&P(G_3)\\
     &&&\ddots\\
     &&&&P(G_K)
     \end{bmatrix}
     $$
     其中 $P(G_i)$ 是 $G_i$ 的可达矩阵。


