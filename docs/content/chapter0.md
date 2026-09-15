# Chapter 0: One Pager on Notations & Quick Refresher

This section contains nothing novel. Most of this would be fairly familiar to most MLEs. So, why put it here? Couple of reasons: (a) I would like to clarify a bit on the notations I've used and (b) in case things are a bit rusty (what was that X thing again?), this is aimed as jogging your memory so you don't have to go back looking these up somewhere else. Things are kept short with almost no explanation as to why these results hold.

## Notations
- $\mathbb{R}$ = Reals
- $\mathbb{R}_{\geq 0}$ = non-negative reals.
- $\mathbb{R}^d$ = d-dimensional real-valued vector space 


## Probability
- We have a sample space $\Omega$ and a vector-valued continuous random variable $X:\Omega\mapsto\mathbb{R}^d$ such that $X(\omega)=\mathbf{x}\in\mathbb{R}^d$.
- Typically boldface characters are used for multidimensional objects (such as $\mathbf{x}\in\mathbb{R}^d$ here), but I've used lowercase $x\in\mathbb{R}^d$ to keep it simple. In this notation, $x=\left(x_1,\cdots,x_d\right)^\top$ with $x_i\in\mathbb{R}$ for all $i=1,\cdots,d$.
- $X\leq x$ applies to every dimension, i.e., $X_i(\omega)\leq x_i$.

### Density & Distribution
- Densities are denoted by lowercase $p$ (e.g., $p_X(x)$ for $p_X:\mathbb{R}^d\mapsto\mathbb{R}_{\geq 0}$), distributions are denoted by uppercase $F$ (e.g., $F_X(x):\mathbb{R}^d\mapsto[0,1]$).

$$
F(x):=\mathbb{P}(X\leq x)=\int\limits_{\{ u\in\mathbb{R}^d\mid u\leq x \}} p(u)\mathop{du}
$$

- I've omitted the subscript $\cdot_X(\cdot)$ as the random variable in our context is always clear from the argument.
- The following holds

$$
  \mathbb{P}(\mathbf{a}\leq X\leq \mathbf{b})=F_X(\mathbf{b})-F_X(\mathbf{a})=\int\limits_\mathbf{a}^\mathbf{b} p_X(\mathbf{x})\mathop{d\mathbf{x}}
$$ 

We only need to recall a handful of results.

### Joint and marginal densities
- Joint density

$$
p_{X,Y}(x,y)=\frac{d}{dx}F_{X,Y}(x,y)
$$

- Marginals are obtained by integrating out one variable.

$$
p_X(x)=\int_{\mathbb{R}}p_{X,Y}(x,y)\mathop{dy}
$$

### Conditional density
- Assuming $p_Y(y) > 0$

$$
p_{X}(x|y)=\frac{p_{X,Y}(x,y)}{p_Y(y)}
$$

- This is a descriptor for probability $\mathbb{P}(X|Y=y)$, implying the only random variable here is $X$, while $Y$ is no longer random (takes a constant value $y$).

### Bayes' theorem

$$
p_{X}(x|y)=\frac{p_{X,Y}(x,y)}{p_Y(y)=\int_{\mathbb{R}}p_{X,Y}(x,y)\mathop{dx}}=\frac{p_Y(y|x)p_X(x)}{\int_{\mathbb{R}}p_Y(y|x)p_X(x)\mathop{dx}}
$$

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
