# Just Enough Calculus

## Frechet Differentiability
Given a function, a useful inquiry regarding it's nature is: what happens to the output of the function when we perturb the input slightly? The goal here is: assuming that the function doesn't behave crazily (i.e., we have some bound on how much it fluctuates for small-enough changes), we can establish certain properties of the functions which can enable us to compute things that would be impossible otherwise.

For scalar functions $f:\mathbb{R}\to\mathbb{R}$ (or $f:\mathbb{C}\to\mathbb{C}$), this is done by considering additive perturbations $x\mapsto x+\delta$, and checking how much it affects the output $f(x)\mapsto f(x+\delta)$. We quantify this by introducing a ratio (since it's possible to compute ratios with scalars) and computing its limit for infinitesimal perturbations:

$$
df\equiv f'(x)\equiv\mathop{\frac{d}{dx}}f:=\lim\limits_{\delta\to 0}\frac{f(x+\delta)-f(x)}{\delta}
$$

With this, the changed output under small-enough perturbations $h$ can be approximated well by a simple multiplication $f'(x)\cdot h$, followed by a simple addition (without having to re-evaluate the function again at $x+h$):

$$
f(x+h)\approx f(x)+f'(x)\cdot h
$$

For functions in general vector space, ratios are not defined. Frechet derivative captures this notion with a slightly different machinery.

Let's assume that we have a function $f:U\to V$, $U$ and $V$ being some vector space where norm is defined (i.e., we can compute length of vectors in these spaces). The same notion of additive perturbations $\mathbf{x}\mapsto\mathbf{x}+\boldsymbol{\delta}$ is considered, causing the output to change $f(\mathbf{x})\mapsto f(\mathbf{x}+\boldsymbol{\delta})$. 

The change in output space is the vector, $\delta\mathbf{f}:=f(\mathbf{x}+\boldsymbol{\delta})-f(\mathbf{x}); \delta\mathbf{f}\in V$, that depends on the perturbation $\boldsymbol{\delta}\in U$ as well as the point we evaluate it (i.e., $\mathbf{x}\in U$). This vector can be thought of being made up by 2 parts - a linear (in $\boldsymbol{\delta}$) part and non-linear part:

$$
\delta\mathbf{f}=\underbrace{g_{\mathbf{x}}(\boldsymbol{\delta})}_{\text{linear}}+\underbrace{h_{\mathbf{x}}(\boldsymbol{\delta})}_{\text{non-linear}}
$$

The idea is: if the non-linear part is negligible, we can ignore it and use the linear part an an approximation of the change vector $\delta\mathbf{f}$. Under this approximation, $h_{\mathbf{x}}(\boldsymbol{\delta})$ then represents the "error" in the approximation. 

To bound the error, we check the ratio of the norms, i.e., $\frac{\lVert h_{\mathbf{x}}(\boldsymbol{\delta}) \lVert}{\lVert \boldsymbol{\delta}\lVert}$. As we reduce the perturbation, if the magnitude of the error stays bounded by the magnitude of the perturbation itself, i.e.,  

$$
\lim\limits_{\boldsymbol{\delta}\to 0} \frac{\lVert h_{\mathbf{x}}(\boldsymbol{\delta}) \lVert}{\lVert \boldsymbol{\delta}\lVert}= 0,
$$

we consider the error to be negligible. In such cases, we consider the function to be "differentiable", use small-oh notation for the error (i.e., $h_{\mathbf{x}}(\boldsymbol{\delta})=o(\lVert\boldsymbol{\delta}\lVert)$), and call $g_{\mathbf{x}}(\boldsymbol{\delta})$ the derivative of the function at $\mathbf{x}$.

$$
\mathop{d\mathbf{f}}=g_{\mathbf{x}}
$$

### Gradient
For scalar valued functions, $f:\mathbb{R}^d\to\mathbb{R}$, the gradient is defined as 

### Jacobian

## Integration
### Multiple Integrals
### Order Swapping
### Change of Variable

## Some More
### Divergence
### Integration By Parts
