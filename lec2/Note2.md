# Lecture 2

## Fast Cut algo
review **Contrast Algorithm** for Min-Cut problem

```{.line-numbers}
Contract Algo:
    Pick an edge uniformly at random;
    Merge the endpoints of this edge;
    Remove self-loops;
    Repeat steps in line 2-4 until only two vertices left;
    The remaining edges form a candidata cut; 
```

time complexity: $O(n^2)$
successful probability: $\Omega(\frac{1}{n^2})$

improvement:
```{.line-numbers}
Fast Cut algorithm: ref Randomized Algo 10.2
Input: multigraph G(V,E)
Output: cut C
    if n <= 6:
         compute min-cut by brute-force enumeration
    else:
        t = [1+n/sqrt2]
        Using Contract algo, perform two independent contract sequences to obtain graphs H1 and H2
        ...each with t vertices
        Recursively compute min-cuts in each of H1,H2
        return the smaller of the two min-cuts

```

Time complexity:
$$T(n)=2T(\frac{n}{\sqrt 2})+O(n^2)$$
$$T(n)=O(n^2\log n)$$
Successful probablity:
the origin size n problem is reduced to two subproblem size $\frac{n}{\sqrt 2}$, considering the contract procedure, the probability that the result of subproblem is exactly the result of origin problem is
$$
(1-\frac{2}{n})(1-\frac{2}{n-1})...(1-\frac{2}{n/\sqrt 2})=\frac{(\frac{n}{\sqrt2}-1)(\frac{n}{\sqrt2}-2)}{n(n-1)}\ge\frac{1}{2}
$$
denote the successful probabilty of origin problem with size n by $P(k+1)$, subproblem with size $\frac{n}{\sqrt 2}$ by $P(k)$, then we have
$$P(k+1)=1-(1-\frac{1}{2}P(k))^2$$
so we get
$$P(k+1)=P(k)-\frac{1}{4}P(k)^2$$
perform a change of variable  $P(k)=\frac{4}{q(k)+1}$, yields the following simplification:
$$q(k+1)=q(k)+1+\frac{1}{q(k)}$$
recursively apply the equation to the righthand side
$$q(k) = q(1)+k-1+\sum_{\mathclap{1\le i\le k-1}} \frac{1}{q(k)}\ge k-1$$
by using $q(k)\ge k-1$,we have
$$q(k)\le q(1)+k-1+\sum_{\mathclap{1\le i\le k-1}} \frac{1}{i} \le q(1)+k-1+\log k$$
combine the upper bound and lower bound
$$q(k)=\Theta(k)$$
$$P(k)=\Theta(\frac{1}{k})$$
observe that $k=\log n$,we can draw the conclution
$$Pr(n)=\Theta(\frac{1}{\log n})$$

### Las Vegas VS. Monte Carlo
* Las Veags: random running time (quick sort)
* Monte Carlo:randomized quality of solution(randomized min cut)


## Complexity Class
only consider ==decision problem== in this chapter

**Definition(P)**:
$L\in P \iff \exists \text{Polynomial  time algorithm A} s.t. \forall x\in \Sigma^*,\begin{cases}x\in L\Rightarrow A(x)accepts\\ x\notin L\Rightarrow A(x)rejects
\end{cases}$

**Definition(NP)**:
$L\in NP \iff \exists \text{Polynomial  time algorithm A} s.t. \forall x\in \Sigma^*,\begin{cases}x\in L\Rightarrow \exists y,|y|=poly|x|,A(x,y)accepts\\ x\notin L\Rightarrow \exists y,|y|=poly|x|,A(x,y)rejects
\end{cases}$

**NP-hard problem(informal definition)**:A is NP-hard ⇔ if A is polynomial time solvable, all problems in NP are polynomial time solvable

**NP-complete**:both NP-hard and in NP

famous NP-complete problems: 3-SAT,Vertex cover,Set cover,Clique,Independent set,integer programming...

