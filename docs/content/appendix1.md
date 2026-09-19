# Just Enough Calculus

## Differentiability
Given a function, a useful inquiry regarding its nature is: what happens to the output of the function when we perturb the input slightly. The goal here is: assuming that the function doesn't behave crazily (i.e., we have some bound on how much it fluctuates for small-enough changes), we can establish certain properties of the functions that enables us to compute things that would otherwise be impossible.

### Scalar Functions
For scalar functions $f:\mathbb{R}\to\mathbb{R}$ (or $f:\mathbb{C}\to\mathbb{C}$), this is done by considering additive perturbations, $x\mapsto x+\delta$, and checking how much it affects the output, $f(x)\mapsto f(x+\delta)$. We quantify this by introducing a ratio (since it's possible to compute ratios with scalars) and computing its limit for infinitesimal perturbations:

$$
df(x)\equiv f'(x)\equiv\mathop{\frac{d}{dx}}f:=\lim\limits_{\delta\to 0}\frac{f(x+\delta)-f(x)}{\delta}
$$

With this, the changed output under "small-enough" perturbations $h$ can be approximated well by performing a simple multiplication $f'(x)\cdot h$, followed by a simple addition. That is, we can claim, without having to re-evaluate the function at $x+h$, that:

$$
f(x+h)\approx f(x)+f'(x)\cdot h
$$

For functions in general vector spaces, ratios are not defined. Frechet derivative captures this notion with a slightly different machinery.

### General Vector-Space: Frechet Differentiability
Let's assume that we have a function $f:U\to V$, where $U$ and $V$ are arbitrary vector spaces with a well-defined norm (i.e., we can compute length of vectors in these spaces). The same notion of additive perturbations $\mathbf{x}\mapsto\mathbf{x}+\boldsymbol{\delta}$ is considered.

The change in output space is the vector, $\delta\mathbf{f}:=f(\mathbf{x}+\boldsymbol{\delta})-f(\mathbf{x})$ (note that $\delta\mathbf{f}\in V$), that depends on the perturbation $\boldsymbol{\delta}\in U$ as well as the point we evaluate it (i.e., $\mathbf{x}\in U$). This vector can be thought of as being made up by 2 parts - a linear (in $\boldsymbol{\delta}$) part and non-linear part:

$$
\delta\mathbf{f}=\underbrace{g_{\mathbf{x}}(\boldsymbol{\delta})}_{\text{linear}}+\underbrace{h_{\mathbf{x}}(\boldsymbol{\delta})}_{\text{non-linear}}
$$

[On the notation: why use subscript for $\mathbf{x}$ and put $\boldsymbol{\delta}$ inside the argument? $\mathbf{x}$ is constant here, as we fix where we want to evaluate this quantity, while we vary only the perturbation $\boldsymbol{\delta}$.]

The motivation behind this decomposition is: if the non-linear part is negligible, we can ignore it and use the linear part as our desired approximation of the change vector $\delta\mathbf{f}$. Under this framing, $h_{\mathbf{x}}(\boldsymbol{\delta})$ then represents the "error" in our approximation. 

To bound this error, we check the ratio of the norms, i.e., $\frac{\lVert h_{\mathbf{x}}(\boldsymbol{\delta}) \lVert}{\lVert \boldsymbol{\delta}\lVert}$ (possible since norms produce reals). As we reduce the magnitude of the perturbation, if the magnitude of the error stays bounded by the magnitude of the perturbation itself, i.e.,  

$$
\lim\limits_{\boldsymbol{\delta}\to 0} \frac{\lVert h_{\mathbf{x}}(\boldsymbol{\delta}) \lVert}{\lVert \boldsymbol{\delta}\lVert}= 0,
$$

then we consider the error to be negligible. We use then use the small-oh notation for the error, i.e.,

$$
h_{\mathbf{x}}(\boldsymbol{\delta})=o(\Vert\boldsymbol{\delta}\Vert)
$$

In such cases, we consider the function to be "differentiable", and call $g_{\mathbf{x}}$ the derivative of the function at $\mathbf{x}$.

$$
\mathbf{df}:=g_{\mathbf{x}}
$$

Note that, as apparent from how it's defined, $\mathbf{df}$ is a function (or, an operator) that has the same shape as $f$, i.e., $\mathbf{df}:U\to V$. It is linear by definition, and it produces $\mathbf{df}(\mathbf{x})\in V$.

### Finite-dimensional Vector-Space: Jacobian
For functions involving finite dimensions (e.g., $f:\mathbb{R}^n\to\mathbb{R}^m$), we can simplify this. In finite dimension, the effect of applying any linear operator can always be achieved by finding a matrix of that operator (there always is one), and then performing simple matrix-vector multiplication.

Let $f'(\mathbf{x})$ be the matrix of the linear operator $\mathbf{df}$. Then, for a sufficiently small-enough perturbation $\mathbf{h}$, the linear approximation becomes

$$
f(\mathbf{x}+\mathbf{h})\approx f(\mathbf{x})+ \mathbf{df}(\mathbf{h})=f(\mathbf{x})+f'(\mathbf{x})\mathbf{h}
$$

We call the matrix the Jacobian matrix, and use $J_{\mathbf{x}}\equiv f'(\mathbf{x})\in\mathbb{R}^{m\times n}$ to represent this quantity. This provides a simplified evaluation rule for our approximation similar to the scalar-case, as $J_{\mathbf{x}}\mathbf{h}$ is simple matrix-vector multiplication.

### Scalar-valued Functions: Gradient
For functions of this form $f:U\to\mathbb{R}$ (or $\mathbb{C}$), if $U$ is equipped with an inner product, then there exists a vector $\boldsymbol{\varphi}_L\in U$ associated with every linear operator $L$, which accomplishes the operation. Therefore, for the derivative, we can write

$$
\mathbf{df}(\mathbf{x})=\langle \boldsymbol{\varphi}_{\mathbf{df}}, \mathbf{x}\rangle
$$

For functions $f:\mathbb{R}^n\to\mathbb{R}$, this equals to the transpose of the Jacobian ($J_{\mathbf{x}}^\top$). We use $\nabla f=\boldsymbol{\varphi}_{\mathbf{df}}$ for this, such that

$$
f(\mathbf{x}+\mathbf{h})\approx f(\mathbf{x})+ \mathbf{df}(\mathbf{h})=f(\mathbf{x})+\nabla f\cdot\mathbf{h}
$$

Here we replaced the inner-product with dot-product.

### Jacobian

## Integration
### Multiple Integrals
### Order Swapping
### Change of Variable

## Some More
### Divergence
### Integration By Parts
