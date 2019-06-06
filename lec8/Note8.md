## Note 8:Combinatory Algorithm

### Knapsack Problem 
Given a set $S = \{a_1,...,a_2\}$ of objects, with specified size and profits ($size(a_i)$ and $profit(a_i)$), and a knapsack capacity B. Find a subset of objects whose total size is bounded by B and total profit is maximized.

**Algorithm 1**: *greedy algorithm*
Sort the objects by decreasing ratio of profit to size, and then greedily pick objects in this order.
$$\frac{p(a_1)}{s(a_1)}\ge \frac{p(a_2)}{s(a_2)} \ge ... \ge \frac{p(a_n)}{s(a_n)}$$
pick $\{a_1,a_2,...,a_k\}$
**Analysis**
The greedy algorithm can be made to perform arbitrarily bad.

**Improvement**
In the last step of the origin algorithm, pick $max\{\{a_1,a_2,...,a_k\},a_{k+1}\}$. This guarantees an approximation ratio of $\frac{1}{2}$


**Algorithm 2**: A pseudo-polynomial time algorithm(DP)
Denote by $f(i,j)$ the minimal size to pick among the first **i** items with total profits **j**.
Then we have$$f(i,j)=min\{f(i-1,j),f(i-1,j-profit(a_i))+size(a_i)\}$$
Initial value$$f(1,0)=0\\f(1,profit(a_1))=size(a_1)$$
The time complexity is $O(n\sum_{i=1}^n profit(a_i))=O(n^2W)$, here $W=max_i \{profit(a_i)\}$

It is a pseudo-polynomial time algorithm because W can be arbitrary large. If $W=poly(n)$, it becomes a polynomial algorithm.
**Algorithm 3**: *rounding technique*
The idea is to ignore a certain number of least significant bits of profits of objects (depending on the error parameter $\epsilon$), the modified profits can be viewed as numbers bounded by $poly(n,\frac{1}{\epsilon})$. This will enable us to find a solution whose profit is at least $(1-\epsilon)OPT$ in time bounded by $poly(n,\epsilon)$

```{.line-numbers}
Algorithm(FPTAS for knapsack)
Given epsilon>0, let K = epsilon*W/n
For each item a_i, profit'(a_i)=[profit(a_i)/K]
use DP to solve the problem with profit', the result is S'
output S'
```
Denote by O the optimal set for origin problem
$$profit(O)-K\times profit'(O)\le nK\\
profit(S')\ge K\times profit'(O)\ge profit(O)-nK=OPT-\epsilon W\ge (1-\epsilon)OPT$$

The time complexity is $O(n^2\lfloor \frac{W}{K}\rfloor)=O(n^2 \lfloor \frac{n}{\epsilon} \rfloor)$

### Complexity Class
To describe approximation algorithm for optimization problems, most ofen NP-hard optimization problems.

**PTAS**: polynomial time approximation scheme, takes an instance of an optimization probelm and a parameter $\epsilon>0$, and in polynomial time, produces a solution that is within a factor $1+\epsilon$ or $1-\epsilon$.

**FPTAS**:in time $poly(n,\frac{1}{\epsilon})$, the approximation ratio is within a factor $1+\epsilon$ or $1-\epsilon$.

**APX**:constant-factor approximation algorithms

**Theorem**
Unless $P=NP$, $FPTAS\subsetneq PTAS \subsetneq APX$

### Steiner Tree
Given an undirected graph $G=<V,E>$ with non-negative edge costs, where vertices are partitione into two sets: Required set R and Steiner set S, find a minimum cost tree in G which contains all the required vertices and subset of Steiner vertices.

*Restricted version*: metric Steiner tree problem (cost function satisfies the triangle inequality)

First, consider the relation between the two versions of Steiner Tree Problem. We prove that if there is a $\epsilon$-approximation algorithm for **metric** Steiner Tree problem, then there is a $\epsilon$-approximation algorithm for Steiner Tree problem.

**Prove**(There is a approximation factor preserving reduction from ST problem to metric ST)

![prove1](assets\1.JPG)
![prove1](assets\2.JPG)

Then, we focus on metric Steiner Problem and give an approximation algorithm.

The approximation algorithm is based on minimum spanning tree (MST).
**Theorem**: The cost of an MST on R is within 2·OPT
**Proof**:
Consider a Steiner tree of cost OPT. By doubling its edges we obtain an Eulerian graph connecting all vertices of R and possibly some Steiner vertices. Find an Euler tour of this graph.
![prove1](assets\3.JPG)
The cost of this Euler tour is 2·OPT. Next obtain a Hamiltonian cycle by traversing the Euler tour and short-cutting
![prove1](assets\4.JPG)
**Tight**
![5](assets\5.JPG)