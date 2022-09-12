The Johnson-Lindenstrauss Lemma

  

**Goal** : Given points $P$ = {$n \in  \mathbb{R}^d$}, describe $P$ in fewer dimensions $k << n, d$. We need to define a function $f$ such that $\forall x_i, x_j \in P $

  

$$||f(x_i) - f(x_j)||_2  \approx ||x_i - x_j||_2$$

  

**Lemma** For any $0 < \epsilon < 1$ and any integer $n$ let $k$ be a positive integer such that

  

$$ k = \Omega\bigg(\frac{log \ n}{3\epsilon^2 - 2\epsilon^3}\bigg)$$

  

then for any set $A$ of $n$ points $\in  \mathbb{R}^d$ there exists a map $f : \mathbb{R}^d \to  \mathbb{R}^k$ such that for all $x_i,x_j \in A$

  

$$(1 - \epsilon)||x_i - x_j||^2  \leq ||f(x_i) - f(x_j)||^2  \leq (1 + \epsilon)||x_i - x_j||^2 \ \ \ w.h.p $$

  

This map can be found in randomized polynomial time. Repeating this projection $O(n)$ times can boost the success probability to any desired constant.

  

**General Outline**

  

- Construct a random projection over $k$ dimensional subspaces.

- Prove that the expected value of euclidean distance of the random projection is equal to the euclidian distance of the original subspace.

- Prove that the variation of the euclidean distance is greater than error factor with very less probability using Markov's Inequality

  

**Formal Proof**

  

Def. Let $R$ be a random matrix of order $k \times d \ i.e \ R_{ij} \stackrel{i.i.d}{\sim} N(0, 1)$ and $u$ be any fixed vector $\in  \mathbb{R}^d .$

  

Defne $v = \frac{1}{\sqrt{k}} R . u$. Thus $v \in  \mathbb{R}^k$ and $v_i = \frac{1}{\sqrt{k}} \sum_j R_{ij}u_j$

  

**Lemma** $E[||v||_2^2] = ||u||_2^2$

  

**Proof**

  

$$
E||v||_2^2 \ \ = \ \ E\bigg[\sum_{i=1}^k v_i^2\bigg]
= \ \ \sum_{i=1}^k E[v_i^2]\\ 
\\
R_{ij}.u_j \sim N(0,u_j^2)\\ 
\\
\sum_{j = 1}^d R_{ij}.u_j \sim N(0,\sum u_j^2)\\ 
\\
\sum_{j = 1}^d R_{ij}.u_j \sim N(0,||u||_2^2)\\ 
\\
= \ \ \frac{1}{k} \sum_{i=1}^k E\bigg[\bigg(\sum_{j = 1}^d R_{ij}.u_j\bigg)^2\bigg]\\ 
\\
Var(X)=E[X^2] - (E[X])^2 \ \ \ \ \because E\bigg[\sum_{j = 1}^d R_{ij}.u_j\bigg] = 0 \\ 
\\
Var\bigg(\sum_{j = 1}^d R_{ij}.u_j\bigg) = E\bigg[\bigg(\sum_{j = 1}^d R_{ij}.u_j\bigg)^2\bigg] = ||u||_2^2\\ 
\\
= \ \ \frac{1}{k} \sum_{i=1}^k||u||_2^2\\
\\
\\
= \ \ ||u||_2^2
$$

  

Def. Let $X = \frac{\sqrt{k}}{||u||}v, \ x = \sum_{i=1}^k x_i^2 = ||X||_2^2 = \frac{k||v||_2^2}{||u||_2^2}$

  

$x_i \sim N(0, 1)$

  

&nbsp;

**Lemma** $P[||v||_2^2  \geq (1 + \epsilon)||u||_2^2] \leq e^{-(\epsilon^2/2 - \epsilon^3/3)k/2}$

  

**Proof**

$$
P [||v||_2^2  \geq (1 + \epsilon)||u||_2^2] \\ 
= P\bigg[\frac{||u||_2^2x}{k} \geq||u||_2^2  \bigg] \\ 
\\
= P[x \geq (1 + \epsilon)k] \\
\\
= P[e^{\lambda x} \geq e^{\lambda (1 + \epsilon)k}] \ \ \ (for \ all \ \lambda  \geq  0)\\
\\
P[x \geq a] \leq  \frac{E[x]}{a} \\
\\
P[e^{\lambda x} \geq e^{\lambda (1 + \epsilon)k}] \leq  \frac{E[e^{\lambda x}]}{e^{\lambda(1 + \epsilon)k}}\\
\\
\leq  \prod_{i = k}^{k} \frac{E[e^{\lambda x_i^2}]}{e^{\lambda(1 + \epsilon)}} \ \ \ (as \ x_i's \ are \ i.i.d.)\\
\\
\\
\leq  \bigg( \frac{E[e^{\lambda x_i^2}]}{e^{\lambda(1 + \epsilon)}}\bigg)^k\\
\\
\leq  \bigg(\frac{1}{\sqrt{1 - 2\lambda} \ e^{\lambda(1 + \epsilon)}}\bigg) ^k \ \ \ \ \ using \ m.g.f \ of \chi^2 \\
\\
put\ \lambda = \frac{\epsilon}{2(1 + \epsilon)}\\
\\
\leq [(1 + \epsilon)e^{-\epsilon}]^{k/2} \\
\\
as \ log(1 + x) \lt x - x^2/2 + x^3/3\\
\\
\leq e^{-(\epsilon^2/2-\epsilon^3/3)k/2}
$$

  

Similarly, $P[||v||_2^2  \leq (1 - \epsilon)||u||_2^2] \leq e^{(-2\epsilon - \epsilon^2/2)k/2}$

  

&nbsp;

  

Finally, $$P[||v||_2^2  \geq (1 + \epsilon)||u||_2^2  \bigcup ||v||_2^2  \leq (1 - \epsilon)||u||_2^2] \leq e^{-(\epsilon^2/2-\epsilon^3/3)k/2} + e^{(-2\epsilon - \epsilon^2/2)k/2}$$

  

$$
P[(1 - \epsilon)||u||_2^2  \leq||v||_2^2  \leq(1 + \epsilon)||u||_2^2] \geq  1 - e^{-(\epsilon^2/2-\epsilon^3/3)k/2} + e^{(-2\epsilon - \epsilon^2/2)k/2}
$$