# Chapter 0: Preliminaries

These should be familiar to most MLEs. Therefore, the content here is meant for a quick refresher.

## Probability
- We're dealing with sample space $\Omega$ and a continuous random variable $X:\Omega\mapsto\mathbb{R}$.
- Densities are defined by lowercase $p$ (e.g., $p_X(x)$ for $p_X:\mathbb{R}\mapsto\mathbb{R}^+$).
- Distribution is defined by uppercase $F$ (e.g., $F_X(x):\mathbb{R}\mapsto[0,1]$) where
- 
$$
F_X(x):=\mathbb{P}(X\leq x)=\int\limits_{-\infty}^x p_X(x)\mathop{dx}

$$
- So, the following holds

$$
  \mathbb{P}(a\leq X\leq b)=F_X(b)-F_X(a)=\int\limits_a^b p_X(x)\mathop{dx}
$$ 

We only need to recall a handful of results.

### Joint and marginal densities

### Bayes' theorem

### Expectations

## Calculus
TODO

Some placeholder math below:
- Dataset: $D=(z_i)_{i=1}^N, z_i\in\mathbb{R}^d$.
- The Goal: Learn a map $T$ that morphs some distribution $p$ to target $q$.

  $$
  T_\sharp p=q
  $$

- Optimal Transport: For some cost function $c:\mathbb{R}^d\times\mathbb{R}^d\to\mathbb{R}_{\geq 0}$

  $$
  \inf_T\mathbb{E}_{x\sim\mu}[c(x, T(x)]
  $$
