# Just Enough Calculus

## Differentiation
Given a function, a useful inquiry regarding its nature is: what happens to the output of the function when we perturb the input slightly. Concretely, considering additive perturbations, $x\mapsto x+\delta$, we check how much it affects the output, $f(x)\mapsto f(x+\delta)$. The goal here is: assuming that the function doesn't fluctuate drastically (i.e., we have some bound on how much it deviates for small-enough changes in the input), we can establish certain properties of the functions that enables us to compute things that otherwise would be impossible. 

### Scalar Functions
For scalar functions $f:\mathbb{R}\to\mathbb{R}$ (or $f:\mathbb{C}\to\mathbb{C}$), this is quantified by introducing a ratio (since it's possible to compute ratios with scalars) and pushing its limit to infinitesimal perturbations. When this limit exists, then we define

$$
f'(x)\equiv\mathop{\frac{d}{dx}}f:=\lim\limits_{\delta\to 0}\frac{f(x+\delta)-f(x)}{\delta}
$$

With this, the changed output under "small-enough" perturbations $h$ can be approximated well by performing a simple multiplication $f'(x)\cdot h$, followed by a simple addition. That is, we can claim, without having to re-evaluate the function at $x+h$, that:

$$
f(x+h)\approx f(x)+f'(x)\cdot h
$$

For functions in general vector spaces, ratios are not defined. Fréchet derivative captures this notion with a slightly different machinery.

### General Normed Vector-Spaces: Fréchet Differentiability
Let's assume that we have a function $f:U\to V$, where $U$ and $V$ are arbitrary vector spaces with a norm (i.e., we can compute length of vectors in these spaces). The change in the output space is the vector, $\delta\mathbf{f}:=f(\mathbf{x}+\boldsymbol{\delta})-f(\mathbf{x})$, that depends on the perturbation $\boldsymbol{\delta}\in U$ as well as the point we evaluate it on (i.e., $\mathbf{x}\in U$). Note that $\delta\mathbf{f}\in V$.

This change vector can be thought of as being made up by 2 parts - a part that changes linearly with $\boldsymbol{\delta}$, and another that captures all the remaining non-linear influences:

$$
\delta\mathbf{f}=\underbrace{L_{\mathbf{x}}(\boldsymbol{\delta})}_{\text{linear}}+\underbrace{E_{\mathbf{x}}(\boldsymbol{\delta})}_{\text{non-linear}}
$$

I used subscript for $\mathbf{x}$ and kept $\boldsymbol{\delta}$ as a parameter since $\mathbf{x}$, being the evaluation-point, is constant here, as we vary only the perturbation $\boldsymbol{\delta}$.

The motivation behind this decomposition is: if the non-linear part is negligible, we can ignore it and use the linear part as our desired approximation of the change vector $\delta\mathbf{f}$. Under this framing, $E_{\mathbf{x}}(\boldsymbol{\delta})$ represents the "error" in our approximation. 

To bound this error, we introduce the ratio of the norms, i.e., $\frac{\lVert E_{\mathbf{x}}(\boldsymbol{\delta}) \lVert}{\lVert \boldsymbol{\delta}\lVert}$ (possible since norms produce reals). As we reduce the magnitude of the perturbation, if the magnitude of the error stays bounded by the magnitude of the perturbation itself, i.e.,  

$$
\lim\limits_{\boldsymbol{\delta}\to 0} \frac{\lVert E_{\mathbf{x}}(\boldsymbol{\delta}) \lVert}{\lVert \boldsymbol{\delta}\lVert}= 0,
$$

then we consider the error to be negligible. We can use the small-oh notation for this error then, i.e.,

$$
E_{\mathbf{x}}(\boldsymbol{\delta})=o(\Vert\boldsymbol{\delta}\Vert)
$$

In such cases, we consider the function to be "differentiable", and call $L_{\mathbf{x}}$ the derivative of the function $f$ at $\mathbf{x}$. 

Note that, as apparent from how it's defined, derivative is a function that has the same domain and codomain as $f$, i.e., $L_{\mathbf{x}}:U\to V$. It is linear by definition, and it produces $L_{\mathbf{x}}(\mathbf{h})\in V$ for $\mathbf{h}\in U$.

Since $L_{\mathbf{x}}$ depends on $\mathbf{x}$, we also define an operator, $\mathbf{df}:\mathbf{x}\mapsto L_{\mathbf{x}}$, that produces this derivative for every $\mathbf{x}$ in domain. This is the differential operator, $\mathbf{df}:U\to (U\to V)$. Using this notation, the approximation becomes

$$
f(\mathbf{x}+\mathbf{h})\approx f(\mathbf{x})+L_{\mathbf{x}}(\mathbf{h})=f(\mathbf{x})+ \left(\mathbf{df}(\mathbf{x})\right)(\mathbf{h})
$$

### Finite-dimensional Vector-Space: Jacobian
For functions involving finite dimensions (e.g., $f:\mathbb{R}^n\to\mathbb{R}^m$), we can simplify this. In finite dimension, the effect of applying any linear function can always be achieved by finding a matrix of that function (there always is one), and then performing simple matrix-vector multiplication.

Let $f'(\mathbf{x})$ be the matrix of the linear function $\mathbf{df}(\mathbf{x})$. Then, for a sufficiently small-enough perturbation $\mathbf{h}$, the linear approximation becomes

$$
f(\mathbf{x}+\mathbf{h})\approx f(\mathbf{x})+ \left(\mathbf{df}(\mathbf{x})\right)(\mathbf{h})=f(\mathbf{x})+f'(\mathbf{x})\mathbf{h}
$$

We call the matrix the Jacobian matrix, and use $J_{\mathbf{x}}\equiv f'(\mathbf{x})\in\mathbb{R}^{m\times n}$ to represent this quantity. This provides a simplified evaluation rule for our approximation similar to the scalar-case, as $J_{\mathbf{x}}\mathbf{h}$ is simple matrix-vector multiplication.

### Scalar-valued Functions on Inner-Product Spaces: Gradient
Let's consider scalar-valued functions $f:U\to\mathbb{R}$ (or $\mathbb{C}$) (called functionals) on complete inner-product spaces $U$ (Hilbert space). For derivatives of such cases, we can use another trick. For any bounded linear functional $L:U\to\mathbb{R}$, there exists a unique vector $\boldsymbol{\varphi}_L$ that achieves the same effect with a simple inner product (Riesz Representation Theorem), i.e., $L(\mathbf{h})=\langle \boldsymbol{\varphi}_L, \mathbf{h}\rangle$. 

For the derivative, we use a special notation $\nabla$ to define this vector, such that 

$$
\nabla_\mathbf{x} f=\boldsymbol{\varphi}_{ L_{\mathbf{x}} }
$$ 

and write

$$
(\mathbf{df}(\mathbf{x}))(\mathbf{h})=\langle \nabla_\mathbf{x} f, \mathbf{h}\rangle
$$

For functions $f:\mathbb{R}^n\to\mathbb{R}$, this equals to the transpose of the Jacobian (as $J_\mathbf{x}$ is the row vector $\mathbb{R}^{1\times m}$)

$$
\nabla_\mathbf{x} f=J_\mathbf{x}^\top
$$

Replacing the inner-product by its finite-dimensional variant, the dot-product, we simplify

$$
f(\mathbf{x}+\mathbf{h})\approx f(\mathbf{x})+f'(\mathbf{x})\mathbf{h}=f(\mathbf{x})+\nabla_\mathbf{x} f\cdot\mathbf{h}
$$



## Integration
### Multiple Integrals
### Order Swapping
### Change of Variable

## Some More
### Divergence
### Integration By Parts
