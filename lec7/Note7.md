# Note7: Approximation Algorithm

### OVERALL
* Decision problem (Yes\No Answer) vs Optimal problem
* Exact algorithm vs Approximation algorithm
* Approximation ratio (Heuristic algo vs Approx algo)

### Maximum Matching
General graph $G=<V,E>$, find the cardinality of maximum matching.
Polynomial time exact algorithm: Blossom_algorithm
**Approximation algorithm**:
```{.line-numbers}
Initialize G' = G, S = NULL
while G' not empty
    randomly choose a vertice v in G' 
    if v has at least one neighbor
        randomly choose a neighbor u
        add <v,u> to S
        remove v & u and associated edges
    else
        remove v 
endwhile
S is the maximum match set
```
**Approximation Analysis**:
$ratio = \frac{1}{2}$, Assume the exact maximum match set is S', for each match $<u,v>$ found in our algorithm, if $<u,v>\notin S'$, then there are at most 2 edges in S' associate with u,v.
The analysis is tight for cases like this:
$$u_1——u_2——u_3——u_4$$

### Vertex Cover
Given graph $G=(V,E)$, find a set $S\subset V$ with minimun cardinality, s.t. $\forall (i,j)\in E$, either $i \in S $ or $j\in S$.
**Approximation Algorithm:**
```{.line-numbers}
Find maximum matching S in G
Add all vertices in S to Vertex Cover
```
First, we prove that the set S of all vertices in maximum matching forms a vertex cover. If there is an edge $<u,v>$ and either u or v is not in S, then it is contradictory to our approx maximum matching algorithm. 
Then we show the approx ratio is 2. For each edge in S, at least one of its endpoints should be included in set cover. The analysis is tight for cases like this:
$$u_1——u_2——u_3$$
Approx: $u_1$  $ u_2$  
Exact : $u_2$

### Set Cover
Given an universal set $U={u_1,u_2,...,u_n}$, m subset $S_1,S_2,...,S_m\subseteq U$ and a cost function c assign each subset to a cost, find set cover with minimum cost.

**Approx Algorithm 1 (Greedy):**
```
While U is not covered
    choose S s.t. min{c(S)/#{new elements covered in S}}
endwhile
```

**Analysis:**
Assume set cover found in our algo is $S_1,S_2,...,S_n$, and the exact answer is $T_1,T_2,...T_n$
Note that
$$\begin{aligned}
\frac{c(S_j)}{|S_j-(S_1\cup S_2\cup ... \cup S_{j-1})|} &\le  \frac{c(S)}{|S-(S_1\cup S_2\cup ... \cup S_{j-1})|}(\forall S)\\
&\le \frac{c(T_i)}{|T_i-(S_1\cup S_2\cup ... \cup S_{j-1})|}(\forall i)\\
&\le \frac{\sum_i c(T_i)}{\sum_i |T_i-(S_1\cup S_2\cup ... \cup S_{j-1})|} (\text{by Sugar Water Ineq})\\
& = \frac{OPT}{\sum_i |T_i-(S_1\cup S_2\cup ... \cup S_{j-1})|}\\
&\le \frac{OPT}{n-|(S_1\cup S_2\cup ... \cup S_{j-1})|} 
\end{aligned}$$
So we can compute the approx result
$$\begin{aligned}
\sum_j c(S_j) &\le OPT \sum_j \frac{1}{n-|(S_1\cup S_2\cup ... \cup S_{j-1})|} \times |S_j-(S_1\cup S_2\cup ... \cup S_{j-1})|\\
&=OPT\times (\frac{1}{n}|S_1|+\frac{1}{n-|S_1|}|S_2-S_1|+\frac{1}{n-|S_1 \cup S_2|}|S_3-(S_1\cup S_2)|)+...\\
&\le OPT\times(\frac{1}{n}+\frac{1}{n-1}+...+\frac{1}{2}+1)\\
&\le OPT\times \ln n
\end{aligned}$$

**Approx Algorithm 2(Layer technique)**:
Define(degree weighted graph):
    there exists constant c, for all v, the weight of vertex v is $c*degree(v)$ 
*Lemma1*: 
for a degree weighted graph, choose all vertices, $\sum_i c(v_i)\le 2*OPT$ 
*Theorem:*
a graph can be decomposed to many degree weighted graphs.

### Inapproximability
* VC is APX-complete: cannot be approximated arbitrarily well unless P=NP
* VC cannot be approximated within a factor of 1.3606 unless P=NP (2005,PCP)
* VC cannot be approximated within a factor of $2-\epsilon$ if unique game conjecture is true 

