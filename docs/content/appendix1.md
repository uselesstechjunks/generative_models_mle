# Just Enough Calculus

## Frechet Differentiability
Given a function, a useful inquiry regarding its nature is: what happens to the output of the function when we perturb the input slightly? The goal here is: assuming that the function doesn't behave crazily (i.e., we have some bound on how much it fluctuates for small-enough changes), we can establish certain properties of the functions which enables us to compute things that would otherwise be impossible.

For scalar functions $f:\mathbb{R}\to\mathbb{R}$ (or $f:\mathbb{C}\to\mathbb{C}$), this is done by considering additive perturbations $x\mapsto x+\delta$, and checking how much it affects the output $f(x)\mapsto f(x+\delta)$. We quantify this by introducing a ratio (since it's possible to compute ratios with scalars) and computing its limit for infinitesimal perturbations:

$$
df(x)\equiv f'(x)\equiv\mathop{\frac{d}{dx}}f:=\lim\limits_{\delta\to 0}\frac{f(x+\delta)-f(x)}{\delta}
$$

With this, the changed output under "small-enough" perturbations $h$ can be approximated well by a simple multiplication $f'(x)\cdot h$, followed by a simple addition. That is, we can claim, without having to re-evaluate the function again at $x+h$, that:

$$
f(x+h)\approx f(x)+f'(x)\cdot h
$$

For functions in general vector spaces, ratios are not defined. Frechet derivative captures this notion with a slightly different machinery.

Let's assume that we have a function $f:U\to V$, where $U$ and $V$ are arbitrary vector spaces where norm is defined (i.e., we can compute length of vectors in these spaces). The same notion of additive perturbations $\mathbf{x}\mapsto\mathbf{x}+\boldsymbol{\delta}$ is considered, causing the output to change $f(\mathbf{x})\mapsto f(\mathbf{x}+\boldsymbol{\delta})$. 

The change in output space is the vector, $\delta\mathbf{f}:=f(\mathbf{x}+\boldsymbol{\delta})-f(\mathbf{x})$ (note that $\delta\mathbf{f}\in V$), that depends on the perturbation $\boldsymbol{\delta}\in U$ as well as the point we evaluate it (i.e., $\mathbf{x}\in U$). This vector can be thought of being made up by 2 parts - a linear (in $\boldsymbol{\delta}$) part and non-linear part:

$$
\delta\mathbf{f}=\underbrace{g_{\mathbf{x}}(\boldsymbol{\delta})}_{\text{linear}}+\underbrace{h_{\mathbf{x}}(\boldsymbol{\delta})}_{\text{non-linear}}
$$

[Clarification on notation used here: why use subscript for $\mathbf{x}$ and put $\boldsymbol{\delta}$ inside the argument? $\mathbf{x}$ is constant here, as we fix where we want to evaluate this quantity, while we vary only the perturbation $\boldsymbol{\delta}$.]

The idea behind this decomposition is: if the non-linear part is negligible, we can ignore it and use the linear part an an approximation of the change vector $\delta\mathbf{f}$. Under this approximation, $h_{\mathbf{x}}(\boldsymbol{\delta})$ then represents the "error" in the approximation. 

To bound the error, we check the ratio of the norms, i.e., $\frac{\lVert h_{\mathbf{x}}(\boldsymbol{\delta}) \lVert}{\lVert \boldsymbol{\delta}\lVert}$. As we reduce the perturbation, if the magnitude of the error stays bounded by the magnitude of the perturbation itself, i.e.,  

$$
\lim\limits_{\boldsymbol{\delta}\to 0} \frac{\lVert h_{\mathbf{x}}(\boldsymbol{\delta}) \lVert}{\lVert \boldsymbol{\delta}\lVert}= 0,
$$

then we consider the error to be negligible. We use the small-oh notation for the error, i.e.,

$$
h_{\mathbf{x}}(\boldsymbol{\delta})=o(\Vert\boldsymbol{\delta}\Vert)
$$

In such cases, we consider the function to be "differentiable", and call $g_{\mathbf{x}}$ the derivative of the function at $\mathbf{x}$.

$$
\mathbf{df}:=g_{\mathbf{x}}
$$

Note that $\mathbf{df}$ has the same dimension as $f$, i.e., $\mathbf{df}:U\to V$, and is linear by definition, and $\mathbf{df}(\mathbf{x})\in V$.

### Jacobian
For functions involving finite dimensions (e.g., $f:\mathbb{R}^n\to\mathbb{R}^m$), we can simplify this, in the same way as scalars. In finite dimension, the effect of applying a linear operator can always be achieved by finding a matrix of that transformation (there always is one), and then performing matrix-vector multiplication.

Let $f'(\mathbf{x})$ be the matrix of the linear map $\mathbf{df}$. Then, for a sufficiently small-enough perturbation $\mathbf{h}$, the linear approximation becomes

$$
f(\mathbf{x}+\mathbf{h})\approx f(\mathbf{x})+ \mathbf{df}(\mathbf{h})=f(\mathbf{x})+f'(\mathbf{x})\mathbf{h}
$$

Here, $f'(\mathbf{x})\in\mathbb{R}^{m\times n}$ is the matrix, typically represented by $J_{\mathbf{x}}$, is called the Jacobian, and $J_{\mathbf{x}}\mathbf{h}$ is simple matrix-vector multiplication.

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
