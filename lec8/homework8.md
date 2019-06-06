# Lecture 8
### 吴昊 2016K8009929015

### 1.Knapsack Greedy algorithm
Prove that the greedy algorithm can be made to perform arbitrarily bad.
**Prove**
Let the capacity bound B = 1, we have two items $a_1$ and $a_2$. $size(a_1)=x$ and $profit(a_1)=2x$,  $size(a_2)=1$ and $profit(a_2)=1$, here $0\lt x \lt 1$.
We have $\frac{profit(a_1)}{size(a_1)}=2\gt \frac{profit(a_2)}{size(a_2)}=1$, according to the greedy algorithm, we should pick $a_1$.The total profit is $2x$, can be arbitrarily small when $x\rightarrow 0$.
However, if we choose $a_2$, the total profit is 1.

### 2.Improvement for Greedy algorithm
Show the approximation ratio of the modifeid algorithm is $\frac{1}{2}$
**Prove**
Assume that 
$$\frac{p(a_1)}{s(a_1)}\ge \frac{p(a_2)}{s(a_2)} \ge ... \ge \frac{p(a_n)}{s(a_n)}$$
Denote by $OPT$ the optimal result, now only need to prove
$$\sum_{i=1}^{k+1}profit(a_i)\ge OPT$$
Which is obvious because $\sum_{i=1}^{k+1} size(a_i)\gt B$, and they are chosen in a greedy way.
Therefore
$$max\{\{a_1,a_2,...,a_k\},a_{k+1}\}\ge \frac{1}{2}OPT$$

### 3.Steiner Tree
Let G=<V,E> be a graph with nonnegative edge costs. S,the senders and R, the receivers, are disjoint subsets of V . The problem is to find a minimum cost subgraph of G that has a path connecting each receiver to a sender (any sender suffices). Partition the instances into two cases: $S \cup R = V$ and $S\cup R \neq V$ . Show that these two cases are in P and NP-hard,respectively. For the second case, give a factor 2 approximation algorithm.

Solve:
$S \cup R = V$ instance:
```{.line-numbers}
Polynomial Algorithm:
T = NULL
while R not empty do
    find a shortest edge e connect a vertex in R (say v) and a vertex in S
    add edge e in T, remove v from R, add v in S
endwhile
```

In *line 3* of each loop, we pick a shortest edge, and this edge must be in the optimal set. This guarantees that the algorithm produces the optimal result.

$S \cup R \neq V$ instance:
First, we show that this problem is NP-hard by reducing original Steiner Tree problem to it.
For a Steiner Tree problem with G=<V,E>, $V=R\cup S$. Select a random vertex in R, say v, let $S'={v}$, $R'=R-v$, S in Steiner Tree problem denotes (V-S'-R') in the new problem.

2-approximation algorithm:
Add a new vertex which is connected to each sender by a zero cost edge. Consider the new vertex and all receivers as required and the remaining vertices as Steiner, and find a minimum cost Steiner tree.
$$result=result(SteinerTree)\le 2·OPT(SteinerTree)=2·OPT$$