# Homework 5
### 吴昊 2016K8009929015（本科生）
### 邮件：wuhao164@mails.ucas.ac.cn


### Randomized Bit Fixing Algo Analysis
Question: In randomized bit fixing algorithm, consider the permutation (x,y)$\rightarrow$(y,x) where x,y are $\frac{n}{2}$-bit string. Prove its running time is $2^\Omega(n)$ with high probability $1-o(1)$

**Prove**:
Let's consider t he permutation $(\vec x,1,\vec y,0)\rightarrow (\vec y,0,\vec x,1)$ rather than $(\vec x,\vec y)\rightarrow (\vec y,\vec x)$, notice that $|\vec x|=|\vec y|=\frac{d}{2}-1$, for simplicity, we will just use x and y.
Now, we try to compute the expectation of routes from (x,1,y,0) to (y,0,x,1) that pass the edge $e:(y,1,y,0)-(y,0,y,0)$
Assume that x and y differ in $c$ bits, if we fix y, there are $\binom{\frac{d}{2}-1}{c}$ different choices of x. A packet will not pass edge e unless it is transported like this: (x,1,y,0)->(y,1,y,0)->(y,0,y,0)->(y,0,x,1). We can compute the expectation of the number of packets passing edge e in such form.
$$\begin{aligned}
E=\sum_{c=0}^{\frac{d}{2}-1} \frac{c!(c+1)!}{(2c+2)!}\binom{\frac{d}{2}-1}{c}&\gt \frac{(\frac{d}{6}-1)!(\frac{d}{6})!}{(\frac{d}{3})!}\frac{(\frac{d}{2}-1)!}{(\frac{d}{6}-1)!(\frac{d}{3})!} \\
&\approx \frac{(\frac{d}{6e})^{\frac{d}{6}}(\frac{d}{2e})^{\frac{d}{2}}}{(\frac{d}{3e})^{\frac{d}{3}}(\frac{d}{3e})^{\frac{d}{3}}}\\
&=(\frac{27}{16})^{\frac{d}{6}}\\
\end{aligned}
$$
Let X denote the number of packets that pass edge e, by applying Chernoff Bound, we have
$$Pr[X\lt \frac{1}{2}E]\lt [\frac{e^{-\frac{1}{2}}}{\frac{1}{2}^{\frac{1}{2}}}]^{2^{\Omega(d)}}=o(1)$$ 

$$Pr[X\gt 2E]\lt [\frac{e}{4}]^{2^{\Omega(d)}}=o(1)$$ 
This yields the result that the running time is $2^\Omega(n)$ with high probability.

### Valiant two-phase algorithm
**Prove**: $Pr(\exists x,delay(x)\gt cn)=o(1)$

In Valiant algorithm, $i$'s packet is sent to $\sigma(i)$ first, then it travels from $\sigma(i)$ to destination $d(i)$. Now, we only focus on phase one: $i$ to $\sigma(i)$
Denote by $p_i$ the path from $i$ to $\sigma(i)$, $p_i=(e_1,e_2,...,e_k),k\le n$    

**Lemma**: For any path $p_i$ and $p_j$, once they separate, they do not rejoin.
*Prove for lemma:* 
If $p_j=(e_1,e_2,e_3',e_4',...,e_l',e_l,...)$, that is $p_j$ and $p_i$ separate at $e_2$ and then rejoin at $e_l$. In that case, there exist $e_{l1}$ and $e_{l2}$, $l_1,l_2\le l$, and $e_{l1}$ is parallel with $e_{l2}$, which is a contradiction.

Let the random variable $H_{ij}=1$ if path $p_i$ and $p_j$ share at least one edge, and 0 otherwise. The total delay of packet i has an upperbound.
$$delay(i)\le n+\sum_{j=1}^N H_{ij}$$
In order to estimate the upper bound of $\sum_{j=1}^N H_{ij}$, we introduce another random variable $T(e)$. Let $T(e)$ denote the number of paths that pass through edge e. For fixed path $p_i=(e_1,e_2,...,e_k)$ with $k\le n$.Then,
$$\sum_{j=1}^N H_{ij}\le \sum_{l=1}^k T(e_l)$$
In class, we have already proved that $T(e_l)=\frac{1}{2}$, which indicates
$$E(\sum_{j=1}^N H_{ij})\le \frac{n}{2}$$
By applying Chernoff Bound, let $H=\sum_{j=1}^N H_{ij}$, we have
$$Pr[H > n]\le Pr[H>2E(H)]\le [\frac{e^1}{2^2}]^{\frac{n}{2}}=(\frac{e}{4})^{\frac{n}{2}} $$
And therefore
$$Pr(delay(x)>2n)\le (\frac{e}{4})^{\frac{n}{2}}$$

### Independent Set
(1)
For each vertex, it remains after deletion with probability $\frac{1}{d}$.
For each edge, it remains only if its two endpoints are not deleted.
$$E(\#vertices)=\frac{n}{d}\\
E(\#edges)=(\frac{1}{d})^2\frac{nd}{2}=\frac{n}{2d}$$
(2)
For all subgraph with $\frac{n}{d}$ vertices, there exists one graph with edges less than or equal with $\frac{n}{2d}$.
For each edge that remains, delete it and delete one of its endpoints.
(3)
*Don't know solution yet.*