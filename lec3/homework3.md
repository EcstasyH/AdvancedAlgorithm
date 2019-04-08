# Homework 2
### 吴昊 2016K8009929015（本科生）
### 邮件：wuhao164@mails.ucas.ac.cn
### 1 Prove Chernoff Bound (2)(3)
Let $X_1,X_2,...,X_n$ be independent Poisson trials such that, for $1\le i \le n, Pr[X_i=1]=p_i$, where $0\lt p_i \lt 1$. Then, for $X=\Sigma_{i=1}^nX_i, \mu=E[X]=\Sigma_{i=1}^np_i$, and any $0 \lt \delta \lt 1$,
$$ Pr[X \lt (1-\delta)\mu]\lt [\frac{e^{-\delta}}{(1-\delta)^{(1-\delta)}}]^\mu\\
Pr[|X-\mu|\gt \delta\mu]\lt 2e^
{-\frac{\delta^2}{3}\mu}$$

**Prove**(2)
For any positive real $\lambda$, and applying Markov inequaity, we have
$$\begin{aligned}
Pr[X\lt (1-\delta)\mu]
=&Pr[-X \gt -(1-\delta)\mu ]\\
=&Pr[e^{-\lambda X} \gt e^{-\lambda(1-\delta)\mu}]\\
\lt&\frac{E[e^{-\lambda X}]}{e^{-\lambda(1-\delta)\mu}} 
\end{aligned}$$
Since $X_i$ are independent, the variable $e^{-\lambda X_i}$ are also independent.
$$
\begin{aligned}
&E[e^{-\lambda X}]\\
=&\prod_{1 \le i \le n}E[e^{-\lambda X_i}]\\
=&\prod_{1 \le i \le n}[p_ie^{-\lambda}+(1-p_i)]\\
=&\prod_{1 \le i \le n}[p_i(e^{-\lambda}-1)+1]\\
\le &\prod_{1 \le i \le n}[e^{p_i(e^{-\lambda}-1)}]\\
=&e^{\mu(e^{-\lambda}-1)}
\end{aligned}
$$
so we have
$$Pr[X\lt (1-\delta)\mu] \lt \frac{e^{\mu(e^{-\lambda}-1)}}{e^{-\lambda(1-\delta)\mu}}$$
let $\lambda = -\ln(1-\delta)$, which is positive, to obtain
$$Pr[X\lt (1-\delta)\mu] \lt \frac{e^{-\mu\delta}}{(1-\delta)^{(1-\delta)\mu}}$$
This yields the desired result.   $\square$

**Prove**(3)
Using McLaurin expansion for $\ln (1-\delta)$ and $\ln (1+\delta)$ to obtain
$$(1-\delta)^{1-\delta} \gt e^{-\delta + \frac{\delta ^2}{2}}\\
(1+\delta)^{1+\delta}>e^{\delta+\frac{\delta^2}{2}-\frac{\delta ^3}{6}}$$
Combine these two inequalities with chernoff bound (1) and (2)

$$
\begin{aligned}
&Pr[|X-\mu|\gt \delta\mu]\\
=&Pr[X\gt (1+\delta)\mu]+Pr[X\lt (1-\delta)\mu]\\
\lt&e^{-\frac{\delta ^2}{2}\mu}+e^{-\frac{\delta ^2}{2}\mu+\frac{\delta ^3}{6}\mu}\\
\lt &2e^{-\frac{\delta ^2}{3}\mu}
\end{aligned}
$$

### 2.bounds for Binomial coefficient 
for integer x range from 1 to m
$$(\frac{m}{x})^x\le\binom{m}{x}\le(\frac{em}{x})^x$$
**Prove:**
$$
\binom{m}{x}=\frac{m}{x}\frac{m-1}{x-1}...\frac{m-x+2}{2}\frac{m-x+1}{1}\ge (\frac{m}{x})^{x}
$$
The other side
$$
\binom{m}{x}=\frac{m}{x}\frac{m-1}{x-1}...\frac{m-x+2}{2}\frac{m-x+1}{1}\le \frac{m^x}{x!}\tag 1
$$
Applying stirling formula $x!=\sqrt{2\pi x}(\frac{x}{e})^x$, since $m(m-1)...(m-x+1)\le \frac{m^x}{\sqrt{2\pi x}}$, we can omit the factor $\sqrt{2\pi x}$ and obtain
$$\binom{m}{x}\le (\frac{em}{x})^x$$

### 3.$Cor(Y_i,Y_j)<0$

