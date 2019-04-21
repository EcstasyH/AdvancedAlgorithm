# Lecture 5

### 掷骰子问题第二问
Q: E(掷出6的步数的期望|掷出6之前数列是不减的)
ANSWER： 2

Prove:
回忆一下几何分布，如果成功概率是p,那么期望下达到平均的步数是$\frac{1}{p}$, 同时也可以知道，期望下失败的次数是$(\frac{1}{p}-1)$
先分析一个最简单的情况，如果只有5、6两个选择，那么
$$E_{56}=E(掷出6的步数的期望|掷出6之前数列是不减的,只有5、6)=？$$
容易知道，这时候，问题等价于几何分布问题，这里掷出5表示失败，掷出6表示成功，所以可知，5出现的次数的期望是1,$E_{56}=2$
进一步分析一个简单的情况，这时我们有4、5、6三个选择，那么此时
$$E_{456}=E(掷出6的步数的期望|掷出6之前数列是不减的,只有4、5、6)=？$$
观察后可以发现，当我们只分析4出现的次数时，同样也等价于一个几何分布，这时，掷出4表示失败，掷出5或者6表示成功，那么成功的概率是$\frac{2}{3}$，因此，4出现的次数的期望是$\frac{1}{2}$。而当第一次出现不是4的数时，5、6出现的概率相等，对应的进入只有6的情况与$E_{56}$对应的情况。
如果用$E_{6}$表示只有6时掷出6需要的次数（显然是1），那么有
$$E_{456}=E(4出现的次数|掷出6之前数列是不减的,只有4、5、6)+E_{56}=\frac{1}{2}+\frac{1}{2}E_{56}+\frac{1}{2}E_{6}=2$$
同理有
$$E_{3456}=E(3出现的次数|掷出6之前数列是不减的,只有3、4、5、6)+\frac{1}{3}E_{456}+\frac{1}{3}E_{56}+\frac{1}{3}E_{6}=\frac{1}{3}+\frac{2}{3}+\frac{2}{3}+\frac{1}{3}=2$$
最终有$E_{123456}=E_{23456}=2$
所以原问题的答案为2。

PS：这道题诡异的地方在于$E_{456}=E_{56}$，看出去前者多了一个4作为“缓冲”，但实际上4作为缓冲区会降低进入$E_{56}$对应的子过程的概率。而且需要注意的是，所有非减的串一定是由6结尾的。

**解法2**：
一个以6结尾的不减序列一定是一下形式$$1\backsim12\backsim23\backsim34\backsim45\backsim56$$
其中，1、2、3、4、5按顺序出现若干次（可能为0），最后6出现1次。我们需要求的就是这种序列长度的期望。
考虑1出现的次数的期望，这是一个成功概率为$\frac{5}{6}$的几何分布，则1平均出现$\frac{1}{\frac{5}{6}}-1=\frac{1}{5}$次。
那么我们继续考虑2平均出现的次数，这里需要注意的是，虽然我们考察的是“出现若干次2之后出现比2大的数字”，但这并不等价于掷一个没有1的骰子。
我们可以先把问题看成，“出现若干次2之后出现不是2就停止”，显然，这个问题答案也是$\frac{1}{5}$. 由于停止时可能出现的末尾数字可能是1、3、4、5、6，而这五种可能概率是相等的，所以，在只出现3、4、5、6的情况下，出现2的次数的期望仍旧是$\frac{1}{5}$.
由此可见，1到5出现的次数的期望均为5，故总的长度的期望是$\frac{1}{5}\times5+1=2$。

### Permutation Routing Problem
see RA C4.2 P74
Given graph G=<V,E>, every node i wants to send one packet to some other node d(i). Every round,every edge direction can transfer at most one packet. How many rounds?
* Permutation：{d(i)} is a permutation
* Oblivious algorithm: the route from i to d(i) depents on (i,d(i)) only.
-----
**Theorem**:
For any deterministic oblivious permutation routing algorithm on a graph of N nodes each of out-degree d, there is an instance of permutation routing requiring $\Omega(\sqrt \frac{N}{d})$ steps.

Ref: "Routing, merging and sorting on parallel models of
computation" by A. Borodin, J.E. Hopcroft. (1985)

----

We only consider n-dimension Boolean hypercube. $N=2^n$ 

**Deterministic Algorithm——Bit Fixing**: scanf the current location and compare it with the destination address. Send the packet out of the current node along the edge corresponding to the leftmost bit in which current position and d(i) differ.

*BAD INSTANCE*:
$$({x_1,...,x_{\frac{d}{2}-1},0,...,0})\rightarrow (\underbrace{0,...,0,1}_{\text{d/2}+1},x_1,...,x_{\frac{d}{2}-1})$$
Congested Edge:$(0,0,...,0)\rightarrow (0,...,0,1,0,..,0)$

**Randomized Bit Fixing**:randomly choose a bit in which the current location and the destination address deffer, then send the packet along the edge corresponding to this bit.

**Two-Phase Randomized Bit Fixing algorithm**(Valiant):
randomly choose a permutation of $[1,n]$, denoted by $\sigma(i)$. The packet is sent to $\sigma(i)$ from $i$, and then send to $d(i)$, by using Bit Fixing algorithm.
**Analysis**:
For an arbitrary edge $e=(\vec a,c,\vec b)to(\vec a,1-c,\vec b),|\vec a|=k,|\vec b|=d-k-1$, we try to compute the expectation of the number of packets that pass edge e.
The source location is denoted by $y$, we want to transport the packet
$$y\rightarrow \sigma(y) \rightarrow d(y)$$
Notice that "$y\rightarrow \sigma(y)$" and"$\sigma(y) \rightarrow d(y)$" are the same, we can only focus on the first step. If edge e is included in the path from $y$ to $\sigma(y)$, $y$ and $\sigma(y)$ should be in the form $y=(\vec d,c,\vec b),\sigma(y)=(\vec a,1-c,\vec f)$. 
Since $\sigma$ is a random permutation
$$Pr(\sigma(y)=(\vec a,1-c,\vec f))=\frac{1}{2^{k+1}}$$
And there are $2^k$ different choices to satisfy $y=(\vec d,c,\vec b)$, so the expection of delay of edge e is $\frac{1}{2}$, average total delay is 1. 
### Probabilistic Method
**Ramsey number**:
    Ramsey number $R(m,n)$ is the smallest number k such that in any 2-coloring of the edges of a complete graph on k vertices by red and blue, there is either a red $K_n$ or a blue $K_m$, computing $R(m,n)$ with exact is difficult, so we are interested in the lower bound.

We already know that $R(2,2)=2$, $R(3,3)=6$, $R(4,5)=25$
$43\lt R(5,5)\lt 49$
*Constructive proof*: $R(m,n)\gt(m-1)(n-1)$ 
*Non-Construct proof* (Paul Erdos):$R(n,n)\ge 2^{\frac{n}{2}}$
**Prove**:
We say a graph G with k vertices is good if there is no red $K_n$ or blue $K_n$
$$\begin{aligned}
    Pr(\text{G is not good})&=Pr(\text{exists red Kn})+Pr(\text{exists blue Kn})\\
    &\le 2Pr(\text{exists red Kn})\\
    &= 2\binom{k}{n}\frac{1}{2^{\binom{n}{2}}}
\end{aligned}$$
When $k=2^{\frac{n}{2}}$, we have Pr(G is not good)<1, so $R(n,n)\gt 2^{\frac{n}{2}}$

**Max Cut**:
For any undirected graph G(V,E) with n vertices and m edges, there is a partition of the vertex set V into 2 sets A and B such that $|{(u,v)\in E},u\in A, v \in B|\ge \frac{m}{2}$
Proof:
Randomly divide the n vertices into 2 subsets. Let $X_i=1$ denote the i-th edge is in the cut.
$$E(|CUT|)=E(\sum X_i)=\sum E(X_i)=\frac{m}{2}$$ 
