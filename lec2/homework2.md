# Homework 
## 2.1 successful prob of Fast-Cut 
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

