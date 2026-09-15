# Part 0: One Pager on Notations & Quick Refresher

Consider this chapter a reference card for the rest of the guide. It grounds our notation and highlights a few standard identities that we will regularly invoke later. It is deliberately brief so you can skim through, get a feel for the notation, and move straight into the core material.

## Notations
- $\mathbb{R}$ = Reals
- $\mathbb{R}_{\geq 0}$ = non-negative reals.
- $\mathbb{R}^d$ = d-dimensional real-valued vector space 

## Calculus in $\mathbb{R}^d$
### Integration as sum
### Integration-by-parts
### Differentiation
### Divergence

## Probability
- We have a sample space $\Omega$ and a continuous random variable capturing $d$ observable real-valued quantities for every event $\omega\in\Omega$.
- This gives a $d$-dimensional vector-valued function as the random variable $X:\Omega\rightarrow\mathbb{R}^d$ such that $X(\omega)=\mathbf{x}\in\mathbb{R}^d$.
- Typically boldface characters are used for multidimensional objects (e.g., $\mathbf{x}\in\mathbb{R}^d$), but I've used lowercase $x\in\mathbb{R}^d$ to keep it simple.
- In this notation, $x=\left(x_1,\cdots,x_d\right)^\top$ with $x_i\in\mathbb{R}$ for all $i=1,\dots,d$.
- Comparison such as $X\leq x$ applies component-wise to every dimension, i.e., $X_i(\omega)\leq x_i$. This is worth calling out since we can't take a proper definition of order in $\mathbb{R}^d$ in the traditional sense, i.e., this does not follow the typical order-axioms.

### Density & Distribution
- Densities are denoted by lowercase $p$ (e.g., $p_X(x)$ for $p_X:\mathbb{R}^d\rightarrow\mathbb{R}_{\geq 0}$), distributions are denoted by uppercase $F$ (e.g., $F_X(x):\mathbb{R}^d\rightarrow[0,1]$).
- I've omitted the subscript $\cdot_X$ at times when the random variable in the context is clear from the argument. I typically write

$$
F(x):=\mathbb{P}(X\leq x)=\int\limits_{\{ u\in\mathbb{R}^d\mid u\leq x \}} p(u)\mathop{du}\equiv\int_{-\infty}^{x_1}\int_{-\infty}^{x_2}\cdots\int_{-\infty}^{x_d} p(u_1,u_2,\cdots,u_d)\mathop{du_1}\mathop{du_2}\cdots\mathop{du_d}
$$

- $X\sim p$ is a shorthand for saying that $X$ has a density $p$.
- I've often used the subscript of the random variable for the density. For example, if we have a random variable dependent on a scalar parameter $t\in\mathbb{R}^d$, such that $X_t:\Omega\rightarrow\mathbb{R}^d; X:(t,\omega)\mapsto x_t\in\mathbb{R}^d$, I've used $X_t\sim p_t$.
- For joint density $p(x, y)$, marginals are obtained by integrating out one variable. I use explicit subscripts for specifying the set of the integration variable, e.g., for $Y$ taking values from $\mathbb{R}^m$

$$
p(x)=\int_{\mathbb{R}^m}p(x,y)\mathop{dy}
$$

### Conditional density
- Assuming $p(y) > 0$

$$
p(x|y)=\frac{p(x,y)}{p(y)}
$$

- This is a density for the event $X|Y=y$, implying the only random variable is $X$, while $Y$ is a constant (no longer random).

### Bayes' theorem

$$
p(y|x)=\frac{p(x|y)p(y)}{\int_{\mathbb{R}^m}p(x|y)p(y)\mathop{dy}}\implies p(y|x)\propto p(x|y)p(y)
$$

- $p(y)$ is called prior and $p(y|x)$ as posterior. $p(x|y)$ is the likelihood.
- $Z=\int_{\mathbb{R}^m}p(x|y)p(y)\mathop{dy}$ is the normalising constant making it a valid probability.

### Expectations
- Expectation of a function $f:\mathbb{R}^d\rightarrow\mathbb{R}^n$ taking values as per the rv $X\sim p$ is defined as the constant

$$
\mathbb{E}_{X\sim p}[f(X)]=\int\limits_{\mathbb{R}^d}f(x)p(x)\mathop{dx}
$$

- Conditional expectation: For $Y$ taking values from $\mathbb{R}^m$, conditional expectation is defined as the deterministic function of $x$. There are various notations typically used for this, such as

$$
\mathbb{E}_{Y\sim p(\cdot|x)}[f(Y)]\equiv\mathbb{E}_{Y|X=x}[f(Y)]\equiv\mathbb{E}[f(Y)|X=x]=\int\limits_{\mathbb{R}^m} f(y) p(y|x)\mathop{dy}=h(x)
$$

- I've used the notation $\mathbb{E}_{Y\sim p(\cdot|x)}[f(Y)]$ in these notes.

### Law of total expectation
- Using the subscript notation for marginal densities, 

$$
\mathbb{E}_{Y\sim p_Y}[Y]=\mathbb{E}_{X\sim p_X}\left[\mathbb{E}_{Y\sim p(\cdot|x)}[Y]\right]
$$

- This follows from

$$
\mathbb{E}_{Y\sim p_Y}[Y]=\int\limits_{\mathbb{R}^m} y\left(\int\limits_{\mathbb{R}^d} p(x,y)\mathop{dx}\right)\mathop{dy}=\iint\limits_{\mathbb{R}^d\times\mathbb{R}^m} y\cdot p(y|x)p(x)\mathop{dx}\mathop{dy}=\int\limits_{\mathbb{R}^d} \left( \int\limits_{\mathbb{R}^m} y\cdot p(y|x)\mathop{dy}\right)p(x)\mathop{dx}=\int\limits_{\mathbb{R}^d} r(x)p(x)\mathop{dx}
$$

- Here $r(x)=\mathbb{E}_{Y\sim p(\cdot|x)}[Y]$. This $r$, known as the regression function, is also the minimiser of the $L_2$ loss

$$
r=\underset{f}{\arg\min}\left(\mathbb{E}_{X,Y\sim p}[\parallel Y-f(X)\parallel_2^2]\right)
$$

## Gaussian Arithmetic
