# Homework 
## 1 successful prob of Fast-Cut 
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
$$q(k)=\Omega(k)$$
$$P(k)=\Omega(\frac{1}{k})$$
observe that $k=\log n$,we can draw the conclution
$$Pr(n)=\Omega(\frac{1}{\log n})$$

## 2 Exercise 10.9
the time complexity of the modified algorithm is $\Theta(n^2+t^3)$ with reducing procedure costs $\Theta(n^2)$ and cubic time algorithm for subproblem.

consider the successful probability,after reducing the problem,the probability that the subproblem result is exactly the origin problem result is

$$
(1-\frac{2}{n})(1-\frac{2}{n-1})...(1-\frac{2}{n/\sqrt 2})=\frac{t(t-1)}{n(n-1)}=\Theta(\frac{t^2}{n^2})
$$

to ensure at least 1/2 successful probabilty,repeat the algorithm $\Theta(\frac{n^2}{t^2})$times

the total running time
$$\Theta(n^2+t^3)*\Theta(\frac{n^2}{t^2})=\Theta(\frac{n^4}{t^2}+n^2t)=\Omega(n^\frac{8}{3})$$
the last step above is by using inequality of geometric and arithmetic means
$$\frac{n^4}{t^2}+\frac{n^2t}{2}+\frac{n^2t}{2}\ge (\frac{n^8}{4})^\frac{1}{3}$$

## Optional(k-way cut-set)

## Exercise 1.10 Page 22
暂时没搞清楚，感觉跟chernoff bound有关系，主要是不知道repeat之后到底怎么操作
## Exercise 1.13 Page 27
**Prove** PP=coPP,
$L\in PP$,$L^c$denote the complement of L. By the definition of PP,there exists an algorithm A,for x in L,Pr(A(x)accepts)>1/2,for x not in L,Pr(A(x)accepts)=0.
construct an algorithm B,B rejects when A accepts,and B accepts when A rejects.
Then $$x\in L^c\Rightarrow Pr(B(x)accepts)=1-Pr(A(x)accepts)\gt \frac{1}{2}$$$$x\notin L^c\Rightarrow Pr(B(x)accepts)=1-Pr(A(x)accepts)\lt \frac{1}{2}$$
which means PP=co-PP

**Prove** BPP=coBPP
assume $L\in BPP$ with algorithm A,construct algorithm B in the same way above.
Then $$x\in L^c\Rightarrow Pr(B(x)accepts)=1-Pr(A(x)accepts)\gt \frac{3}{4}$$$$x\notin L^c\Rightarrow Pr(B(x)accepts)=1-Pr(A(x)accepts)\lt \frac{1}{4}$$
implys BPP=co-BPP

## Optional Problem 1.15 Page 27

