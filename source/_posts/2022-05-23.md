---
title: 通路与回路
math: true
date: 2022-05-24 22:31:50
categories: 课程笔记
tags: 离散数学
index_img:
banner_img:
---


**通路**：设$G$为无向图，顶点和边的交替序列$\Gamma = v_{i_0}e_{j_0}v_{i_1}e_{j_1}...e_{j_l}v_{i_l}$称为$v_{i_0}$到$v_{i_l}$的**通路**，$e$ 是  $v$ 顶点连接的边

**始点：**$v_{i_0}$   		**终点：**$v_{i_l}$
**长度**：通路中边的条数

-   **简单通路**：$\Gamma$中所有边互异（即通路中边只出现一次，点可以重复通过）
-   **初级通路(路径)**：$\Gamma$中所有边互异，所有顶点互异（即通路中的顶点和边只出现一次）
-   **复杂通路**：$\Gamma$中有边重复



**回路**：<u>始点和终点相同</u>的通路

-   **简单回路**：始点和终点相同的简单通路
    
-   **初级回路（圈）**：始点和终点相同的初级通路
    -   奇圈：长度为奇数的圈
        
    -   偶圈：长度为偶数的圈
    
-   **复杂回路**：始点和终点相同的复杂通路

表示方法：$\Gamma = v_{i_0}e_{j_0}v_{i_1}e_{j_1}...e_{j_l}v_{i_l}$

---


含**圈**的无向图 $G$中

-   **周长**：$G$ 中最长圈的长度，记作 $c(G)$
-   **围长**： $G$ 中最短圈的长度，记作 $g(G)$



**定理 7.6**：

在 $n$ 阶图 $G$ 中，若从顶点 $v_i$ 到 $v_j$（$v_i  \neq v_j$）存在通路，则从 $v_i$ 到 $v_j$ 存在长度 $\leq(n-1)$ 的通路。

+ **推论**：

  在$n$阶图$G$中，若从顶点 $v_i$ 到 $v_j$（$v_i  \neq v_j$）存在通路，则从 $v_i$ 到 $v_j$ 一定存在长度 $\leq(n-1)$ 的路径（初级通路）。



**定理 7.7**：

在 $n$ 阶图 $G$ 中，若存在 $v_i$ 到自身的回路，则存在 $v_i$ 到自身长度 $\leq n$ 的回路。

+ **推论**：

  在 $n$ 阶图 $G$ 中，若存在 $v_i$ 到自身的<u>简单回路</u>，则存在 $v_i$ 到自身长度 $\leq n$ 的<u>初级回路（圈）</u>。



:cactus: **扩大路径法**



无向图的连通性
----
**定义 7.20**：

设$G=<V,E>,\forall u, v \in V$，若$u，v$之间存在通路，则称$u，v$是连通的，记作 $u \sim v$
> 无向图中顶点之间的连通关系是等价的
$R=\{<u,v>|u,v\in V 且 u~v\}$



+ **连通图**：G为平凡图或G中任何两个顶点都是连通的

+ **非连通图（分离图）**：没有顶点连通

+ **连通分支**：V关于R的等价类的导出子图。
  $V/R=\{V_1,V_2,...V_k\}$称$G[V_1],G[V_2],...G[V_k]$为$G$的连通分支，连通分支数记作$p(G)$.

  > **G是连通的**：p(G) = 1 $\Longrightarrow$G是平凡图或者任意两结点都是连通的
  > **非连通图或分离图**：$p(G) \geq 2$
  
+ **短程线**：u,v之间长度最短的通路。

  + **距离**：短程线的长度，记$d(u,v)$
  + $u, v$ 不连通时 $d(u,v)=\infty$

  > ![](https://ftp.bmp.ovh/imgs/2021/04/6b1b8720a76169c1.png)

+ **直径**：设图$G=<V,E>$称$max\{d(u,v) | u,v \in V\}$为G的直径，记作$d(G)$
  $\iff$图中最大的距离

##### 定理 7.8

**一个图 G 为二部图 **$\iff$ **图 G 中无奇圈**。



##### 定理 7.9

设 G 为 n 阶无向图， 若 G 是连通图， 则 G 的边数 $m \ge n - 1.$

> <img src="https://ftp.bmp.ovh/imgs/2021/04/d1e28657d6657eb7.png" style="zoom:50%;" />





无向图的连通度
----

+ **点割集**：点的集合，删除该点后能够增加连通分支数。
  ![](https://ftp.bmp.ovh/imgs/2021/04/d0aa2d8eb10faa46.png)

+ **边割集（割集）**：边的集合，删除该边后能够增加连通分支数。
  ![](https://ftp.bmp.ovh/imgs/2021/04/c3dd9be12404f0ad.png)

-   **扇形割集**
    <img src="https://ftp.bmp.ovh/imgs/2021/04/192315b133a67995.png" style="zoom:50%;" />

**点连通度**：设G为无向简单图且不含$K_n$为生成子图，则称$\kappa (G)=min\{|V'|  V'为G的点割集\}$为**点连通度**，简称*连通度*。

> G是**k-连通图**: $\kappa(G)\ge k$ 
> 规定: $κ(K_n) = n-1, G非连通: κ(G)=0$
>
> <img src="https://ftp.bmp.ovh/imgs/2021/04/5135ef66cc29f58b.png" style="zoom: 50%;" />



**边连通度**：设G是无向连通图，称$\lambda (G)=min\{|E'|  E'是G的边割集\}$为G的**==边连通度==**

> <img src="https://ftp.bmp.ovh/imgs/2021/04/3671498445fa59f4.png" style="zoom: 50%;" />
##### **定理 7.10 （Whitney）**

**对任意图 G，$\kappa(点连通度) \leq\lambda(边连通度）\leq \delta（最小度）$**

+ **引理 1**: 设E’是边割集,则  $p(G-E’)=p(G)+1$.

  > 即 删除边割集的+边后，图的连通分支加一

+ **引理2**: 设 $E’$ 是非完全图 $G$ 的边割集,  $λ(G)=|E’|$ ,  $G-E’$ 的2个连通分支是 $G1,G2$，则 存在 $u∈V(G1), v∈V(G2)$，使得  $(u,v)∉E(G)$​.
  + **推论**：若 G 是 k-连通图，则 G 是 k边-连通图



##### **定理 7.11**

G 是 n （$\geq 6$）阶简单无向连通图，$\lambda(G) < \delta(G)$，则存在图$G*$，它是以$G$为生成子图，$G*$由完全图$K_{n_1}$和$K_{n-{n_1}}$，以及他们之间的$\lambda(G)$条边组成，$\lambda(G)+2 \leq n_1 \leq \lfloor n \rfloor$。（$\lfloor n \rfloor$是下取整，$\lceil n \rceil$上取整）

<img src="https://ftp.bmp.ovh/imgs/2021/04/997eabc25154d5ca.png" style="zoom:50%;" />
![](https://ftp.bmp.ovh/imgs/2021/04/b26c59dcb4284ae3.png)

+ **推论：**当$\lambda(G) < \delta(G)$，
  1. $\delta(G) \leq \delta (G*) \leq n_1 - 1 \leq \lfloor \frac{n}{2} \rfloor - 1$
  2. $G*$中有不相邻顶点$u,v$，使得$d_{G*}(u)+d_{G*}(v)\leq n-2$
  3. $d(G)\geq d(G*) \geq 3$



##### 定理 7.12 ($\lambda = \delta$的充分条件)

+ G 是 6 阶及以上连通简单无向图。
  1. $\delta(G) \geq \lfloor \frac{n}{2} \rfloor \Longrightarrow \lambda(G) = \delta(G)$
  2. 若任意一对不相邻顶点$u,v$，都有$d(u)+d(v)\geq n-1$，则$\lambda(G) = \delta(G)$
  3. $d(G)\leq2 \Longrightarrow \lambda(G) = \delta(G)$



+ **Whitney:** $κ≤λ≤δ$. 
  + 当 $λ(G)<δ(G)$, 有（定理11的推论） 
    1. $\delta(G) \leq \lfloor \frac{n}{2} \rfloor - 1$
    2. $\exist  u,v \in V(G)$，使得  $d_G(u)+d_G(v) \leq n-2$
    3. $d(G)\geq 3$
  + 当$λ(G)=δ(G)$的充分条件如下：（定理12） 
    1. $\lambda(G)\geq \lfloor \frac{n}{2} \rfloor$
    2. $\forall u,v\in V(G)$，使得$d_G(u)+d)G(v)\geq n-1$
    3. $d(G)\leq2$



##### 定理 7.13

设 G 是 n 阶**无向简单连通非完全图**，则$\kappa(G) \ge2\delta(G)-n+2$.



##### 定理 7.14

对于给定的正整数$n,\delta,\kappa,\lambda$，存在n阶简单连通无向图G，$\delta(G)=\delta, \kappa(G)=\kappa,\lambda(G)=\lambda \iff$
+ $\delta < \lfloor \frac{n}{2}\rfloor$：$0 \leq \kappa \leq \lambda \leq \delta \ <\lfloor \frac{n}{2}\rfloor$
+ $\delta \geq \lfloor \frac{n}{2}\rfloor$，G 是非完全图时：$1\leq2\delta-n+2\leq\kappa\leq\lambda=\delta \leq n-1$
+ $\delta \geq \lfloor \frac{n}{2}\rfloor$，G 是完全图时：$\kappa =\lambda = \delta = n-1$



#####  定理 7.15 （2-连通的充分必要条件）

设G为$n(n\ge3)$阶无向连通图，G为2-连通图$\iff$G中任意两个顶点共圈

+ **独立路径**：两条除起点和终点外无其他公共顶点的路径。
+ **定理 15’**：3 阶以上无向简单连通图 G 是2 - 连通图$\iff$G 中任意两个顶点之间有两条以上独立路径。



**定理 16  2-边连通的充分必要条件**

3阶以上无向图G是2-边连通图$\iff$G中任意两 个顶点共简单回路. 

+ **边不交(edge-disjoint)路径**: 两条无公共边(但可能有公 共顶点)的路径. 
+ **定理16’**:  3阶以上无向图G是2-边连通图$\iff$G中任意两 个顶点之间有两条以上边不交路径。



**k-(边)连通的充分必要条件**

+ **定理:** 3阶以上无向图G是k-连通图$\iff$G中任意两个顶点之间有k条以上独立路径。 
+ **定理:** 3阶以上无向图G是k-边连通图$\iff$G中任意两个顶点之间有k条以上边不交路径。



**割点的充分必要条件**

+ **定理17** ：无向连通图G中顶点v是割点$\iff$可以把$V(G)-{v}$ 划分成$V_1$与$V_2$,使得从$V_1 $中任意顶点u到$V_2$中任意顶点$w$ 的路径都要经过v.  
+ 推论： 无向连通图G中顶点v是割点$\iff$存在与v不同的顶点u和w,使得从顶点u到w的路径都要经过v. 



+ **定理18** 无向连通图G中边e是桥$\iff$G的任何圈都不经过e.  
+ **定理19** 无向连通图G中边e是桥$\iff$可以把V(G)划 分成$V_1$与$V_2$,使得从$V_1$中任意顶点u到$V_2$中任意顶点v的路径都要经过e. 



##### 定义 7.29 块



**定理20: **

G是3阶以上无向简单连通图，则G是块 

$\iff$G中任意2顶点共圈 

$\iff$G中任意1顶点与任意1边共圈

$\iff$G中任意2边共圈

$\iff$G中任意2顶点与任意1边,有路径连接这2顶点并经 过这1边

$\iff$G中任意3顶点,有路径连接其中2顶点并经过第3点 

$\iff$G中任意3顶点,有路径连接其中2顶点并不经过第3点.



---

###  补充

1.  G是n阶无向简单图
   + 当 $\delta(G)\geq \frac{n}{2}$， G`是连通图`
   + 当$\delta(G) \geq \frac{1}{2}(n+k-1)$，G是`k-连通图`