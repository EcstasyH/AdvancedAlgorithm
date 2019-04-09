# Lecture 3

## Useful inequality
**Union Bound**
Let $E_i$ be a random event, then we have $Pr[\cup_{i=1}^nE_i]\le \sum_{i=1}^nPr(E_i)$


**Markov inequality**
Let Y be a random variable assuming only non-negative values. Then for all $t\gt0,Pr[Y\ge t]\le\frac{E[Y]}{t}$

**Chebyshev inequality**
Let X be a random variable with expectation $\mu_x$ and standard deviation $\sigma_X$, then for any $t\gt 0,Pr[|X-\mu_X|\ge t\sigma_X]\le \frac{1}{t^2}$

**Chernoff bound**
Let $X_1,X_2,...,X_n$ be ==independent Poisson trials== such that, for $1\le i \le n, Pr[X_i=1]=p_i$, where $0\lt p_i \lt 1$. Then, for $X=\Sigma_{i=1}^nX_i, \mu=E[X]=\Sigma_{i=1}^np_i$, and any $\delta\gt 0$,
$$Pr[X\gt (1+\delta)\mu]\lt [\frac{e^\delta}{(1+\delta)^{(1+\delta)}}]^\mu$$
... and any $0 \lt \delta \lt 1$,
$$Pr[X \lt (1-\delta)\mu]\lt [\frac{e^{-\delta}}{(1-\delta)^{(1-\delta)}}]^\mu\\Pr[|X-\mu|\gt \delta\mu]\lt 2e^
{-\frac{\delta^2}{3}\mu}$$

Prove：
for any positive real $\lambda$, and applying Markov inequaity, we have
$$\begin{aligned}
&Pr[X\gt (1+\delta)\mu]\\
=&Pr[e^{\lambda X} \gt e^{\lambda(1+\delta)\mu}]\\
\lt &\frac{E[e^{\lambda X}]}{e^{\lambda(1+\delta)\mu}} 
\end{aligned}$$
consider $E[e^{\lambda X}]$, since $X_i$ are independent, the variable $e^{\lambda X_i}$ are also independent.
$$
\begin{aligned}
&E[e^{\lambda X}]\\
=&\prod_{1 \le i \le n}E[e^{\lambda X_i}]\\
=&\prod_{1 \le i \le n}[p_ie^\lambda+(1-p_i)]\\
=&\prod_{1 \le i \le n}[p_i(e^\lambda-1)+1]\\
\le &\prod_{1 \le i \le n}[e^{p_i(e^\lambda-1)}]\\
=&e^{\mu(e^\lambda-1)}
\end{aligned}
$$
so we have
$$Pr[X\gt (1+\delta)\mu]\lt \frac{e^{\mu(e^\lambda-1)}}{e^{\lambda(1+\delta)\mu}}$$
let $\lambda = \ln(1+\delta)$
$$Pr[X\gt (1+\delta)\mu]\lt \frac{e^{\mu\delta}}{(1+\delta)^{(1+\delta)\mu}}$$
This yields the desired result.   $\square$

There are three main ingredients in the above proof:
1. We studied the random variable $e^{\lambda X}$ rather than $X$.
2. The expectation of the product of the $e^{\lambda X_i}$ turns into the product of their expectations owing to independence.
3. We pick a value of $\lambda$ to obtain the best possible upper bound, and it depends on the deviation $\delta$.

PS: The other two forms of Chernoff bound are proved in Homework.

## Balls and Bins
  * m balls, n bins. randomly throw each ball to some bin
  * Xi denote the number of balls in i-th bin
  * let $k=max\{Xi\}$
  
Question:expectation and distribution of k?
1. $m=o(\sqrt n)$,$Pr(k>1)=?$
2. $m=\Theta (\sqrt n)$,$Pr(k>1)=?$
3. $m=n$, find x s.t. $Pr(k\le x)=1-o(1)$ and prove $k=\Theta(\frac{n \ln n}{\ln \ln n})$ w.h.p(with high probability)
4. $m\ge n\ln n$

**The first question** is when ==$m=o(\sqrt n)$==, we try to compute Pr(k>1), which is the probability that more than two balls fall into one same bin.
Observe that
$$Pr(k\gt1)=Pr(X_1\ge 2 \bigvee X_2 \ge 2 \bigvee ...\bigvee X_n\ge 2)\tag1$$
By applying the Union Bound inequality to the right side, we have
$$Pr(k \gt 1)\le n Pr(X_i\gt 2)\tag2$$
The question reduces to how to compute $Pr(X_i\gt 2)$, we can give it an upper bound
$$Pr(X_i\ge 2)\lt \binom{m}{2}(\frac{1}{n})^2\tag3$$
Obsever that
$$n\binom{m}{2}(\frac{1}{n})^2=\frac{m(m-1)}{2n}\tag4$$
Since $m=o(\sqrt n)$, we get 
$$Pr(k>1)\lt o(\frac{1}{2})$$

**The second question** is when ==$m=\Theta(\sqrt n)$==, how can we compute $Pr(k>1)$. Assume $m=c\sqrt n$ and (4) again gives an upper bound. 
$$Pr(k>1)\lt \frac{c^2}{2}$$
Actually, we can compute $Pr(k=1)$ exactly.
$$\begin{aligned}
Pr(k=1)=&\frac{n-1}{n}\frac{n-2}{n}...\frac{n-m+1}{n}\\
=&(1-\frac{1}{n})(1-\frac{2}{n})...(1-\frac{m-1}{n})\\
\lt&e^{-\frac{1}{n}-\frac{2}{n}-...-\frac{m-1}{n}}\\
=&e^{-\frac{c^2}{2}}
\end{aligned}\tag5$$
Which gives $Pr(k\ge 2)$ a lower bound. 

**The $m=n$ case** is more complex, we try to find suitable x such that $k=\Theta(x)$ with high probability,i.e.
$$Pr(k\le x)=1-o(1)\\Pr(k\ge cx)=o(1)\tag 6$$
$Pr(k\ge x)$ have an upper bound by using Union Bound.
$$Pr(k\ge x)\le n\binom{n}{x}(\frac{1}{n})^x\tag7$$
We know that 
$$(\frac{n}{x})^x\le \binom{n}{x} \le (\frac{en}{x})^x\tag 8$$
So we have 
$$Pr(k\ge x)\le n(\frac{e}{x})^x\tag 9$$
Take $x=\frac{\ln n}{\ln \ln n}$ into (9), we can obtain that $Pr(k\ge x)=o(1)$. Then we want $Pr(k\le cx)=o(1)$ 

$$Pr(k\le cx)=Pr(X_1\le cx \bigwedge X_2\le cx \bigwedge ... \bigwedge X_n\le cx)\tag{10}$$
We then try to use Chebyshev inequality: denote $X_i\le cx$ by $Y_i=0$, otherwise $Y_i = 1$
$$\begin{aligned}
Pr(k\le cx)=&Pr(\forall i,Y_i=0)\\
\le&Pr(|\sum_{i=1}^nY_i-E(\sum_{i=1}^nY_i)|\ge E(\sum_{i=1}^nY_i))\\
\le& \frac{\sigma^2(\sum_{i=1}^nY_i)}{E(\sum_{i=1}^nY_i)^2}\tag{11}
\end{aligned}$$
Compute the expectation and take $x=\frac{\ln n}{\ln \ln n}$ 
$$\begin{aligned}
E(\sum_{i=1}^nY_i)=& nPr(X_i\gt cx)\\
\ge&nPr(X_i=cx)\\
=&n \binom{n}{cx}(\frac{1}{n})^{cx}(1-\frac{1}{n})^{n-cx}\\
\ge &n(\frac{n}{cx})^{cx}(\frac{1}{n})^{cx}(\frac{1}{e})^{\frac{n-cx}{n}}\\
\ge &n(\frac{1}{cx})^{cx}\frac{1}{e}\\
=& \Theta(n^{1-c})
\end{aligned}$$

To compute $\sigma^2$, need to specify that $Cor(Y_i,Y_j)<0$, and $p_i$ denote the probability that $Y_i=1$ 
$$\begin{aligned}
&Var(\Sigma_{i=1}^nY_i)\\
=&\Sigma_{i=1}^nVar(Y_i)\\
=&\Sigma_{i=1}^n(p_i-p_i^2)\\
\le& n
\end{aligned}$$
so
$$Pr(k\lt cx)\le O(\frac{n}{n^{2(1-c)}})$$
let $c=\frac{1}{3}$,we can say $\frac{\ln n}{3\ln \ln n}\lt k \lt \frac{\ln n}{\ln \ln n}$ with high probability.

What about $m\ge n\ln n$? We can prove $k=\Theta(\frac{m}{n})$ w.h.p.

$$\begin{aligned}
Pr(k\ge c\frac{m}{n})\le& n\binom{m}{c\frac{m}{n}}(\frac{1}{n})^{c\frac{m}{n}}\\
\le&n(\frac{em}{c\frac{m}{n}})^{c\frac{m}{n}}(\frac{1}{n})^{c\frac{m}{n}}\\
=& n(\frac{e}{c})^{c^2\ln n}\\
=&o(1)  
\end{aligned}$$
Need $(\frac{e}{c})^{c^2}\lt \frac{1}{e}$. Or we can use Chernoff bound to prove. Let $Y_i$ denote that the i-th ball fall into the first bin.(which bin does not matter) 
$$X_1=\Sigma_{i=1}^mY_i$$
$$Pr(|X_1-\frac{m}{n}|\lt c_1\frac{m}{n})\le 2e^{-\frac{c_1^2}{3}\frac{m}{n}}=2\frac{1}{n^{\frac{c_1^2}{3}}}$$