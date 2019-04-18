# Lecture 4

### 一道有趣的概率问题
为了叙述更清晰，这一段使用中文。
**题目：
对于一个筛子(6个面，1-6)，连续掷若干次，当第一次朝上的面是6时就停止，我们知道抛掷次数的期望是6,即E(首次出现6需要的次数)=6，现在我们需要求
$$E(首次出现6需要的次数|掷出的都是偶数)$$PS：答案不是3**

解法1：
先看$Pr(掷出的均为偶数)$
$$Pr(掷出的均为偶数)=\sum_{i=1}^{\infty}Pr[第i次出现6，前面均为2，4]$$
$$E=\frac{\sum_{i=1}^{\infty}i\times Pr[第i次出现6，掷出的均为偶数]}{Pr(掷出的均为偶数)}=\frac{\sum_{i=1}^{\infty}i\frac{1}{6}(\frac{1}{3})^{i-1}}{\sum_{i=1}^\infty \frac{1}{6}(\frac{1}{3})^{i-1}}=\frac{3}{2}$$

PS:
一个常见（**但是错误**）的思路是，把这个骰子看成只有3个面，分别是2、4、6，那么需要求的期望等价于掷这个骰子首次出现6的期望，这是一个几何分布，每次出现6的概率都是$\frac{1}{3}$.
分析一下“三面骰子”的错误，我认为在于分析Pr[第i次出现6|掷出的均为偶数]时，分母多乘了$\frac{1}{2}$，实际上，以为我们指定了第i次出现6，所以只需要要求前面的（i-1）次都是偶数即可。

解法2：
换一个对题目的表述
**不断扔一个等概率的骰子，直到扔出1、3、5、6停止，求最后一次扔出6条件下扔骰子次数的期望**
这是一个系数为$\frac{2}{3}$的几何分布。期望为$\frac{3}{2}$，由于1、3、5、6是对称的，所以在最后一次是6的条件下期望不会改变，仍为$\frac{3}{2}$

### Coupon Collector's Problem
In **balls and bins** problem, try to find m s.t. $Pr(min\{X_1,X_2,...,X_n\}\ge 1)=1-o(1)$, that is to guarantee each bin has more than one ball with high probability.
$$Pr(\exists i,X_i=0)\le nPr(X_i=0)=n(\frac{n-1}{n})^m=o(1)$$
So we want $(\frac{n-1}{n})^m=o(\frac{1}{n})$,let $m=n \ln n$

**Another method**
Let T denote the least number of balls to satisfy that each bin has more than one ball, while $Z_i$ denote the number of balls needed to create the i-th unempty bin.
$$T=Z_1+Z_2+...+Z_n$$
$$Z_i=\frac{n}{n-i+1}$$
so we have
$$E(T)=n\ln n$$
$$Var(T)=Var(\Sigma_{i=1}^nZ_i)=\Sigma_{i=1}^nVar(Z_i)=\Theta(n^2)$$
Applying the Chebyshev inequality
$$Pr(|T-n\ln n|\ge c'n\ln n)\le \frac{\Theta(n^2)}{(c'n\ln n)^2}=o(1)$$

### Deferred principle
课上讲了三个问题，描述起来比较麻烦，解题过程主要都是口头表述的，所有笔记不完整，在下面记录题目

1 飞机座位问题
有n个座位，对应编号1到n，有n个人，除了第一个人外每个人有一个号码牌，彼此号码不相同。现在，第一个人首先随便选一个位置坐下，之后由第二个到第n个人依次选择座位，选择方式如下，如果自己的号码牌对应的位置是空的，则坐在该位置上，否则随便选一个位置坐。
问：第n个人坐在自己的座位上的概率是多少？

2 扑克牌问题
一副扑克牌把王牌去除，剩余52张，把J、Q、K认为是11、12、13，则剩余4组1-13.现在按如下方式操作：
1. 将52张牌随机分成13组，每组4张牌，面朝下覆盖
2. 从第一组中抽出一张牌
3. 假设抽出的牌是i，则接着从第i组抽出一张牌
4. 重复第三步，直到某一次抽到的牌指向的那一组已经没有剩余牌了

问：把所有牌抽完的概率是多少？ 