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

then we consider the error to be negligible. We can use the small-oh notation for this error then, i.e., $E_{\mathbf{x}}(\boldsymbol{\delta})=o(\Vert\boldsymbol{\delta}\Vert)$, and write

$$
f(\mathbf{x}+\mathbf{h})=f(\mathbf{x})+L_{\mathbf{x}}(\mathbf{h})+o(\Vert\boldsymbol{\delta}\Vert)
$$

In such cases, we consider the function to be "differentiable", and call $L_{\mathbf{x}}$ the derivative of the function $f$ at $\mathbf{x}$. 

Note that, as apparent from how it's defined, derivative is a function that has the same domain and codomain as $f$, i.e., $L_{\mathbf{x}}:U\to V$. It is linear by definition, and it produces $L_{\mathbf{x}}(\mathbf{h})\in V$ for every $\mathbf{h}\in U$.

### Differential Operator
Since the derivative $L_{\mathbf{x}}$ depends on $\mathbf{x}$, we can also identify an operator, $\mathbf{df}:\mathbf{x}\mapsto L_{\mathbf{x}}$, that produces this derivative for every $\mathbf{x}$ in domain. This is the differential operator, $\mathbf{df}:U\to (U\to V)$. Using this notation, the approximation becomes

$$
f(\mathbf{x}+\mathbf{h})\approx f(\mathbf{x})+L_{\mathbf{x}}(\mathbf{h})=f(\mathbf{x})+ \left(\mathbf{df}(\mathbf{x})\right)(\mathbf{h})
$$

### Finite-dimensional Euclidean Vector-Space: Jacobian
For functions involving finite dimensions (e.g., $f:\mathbb{R}^n\to\mathbb{R}^m$), we can simplify this. In finite dimension, the effect of applying any linear function can always be achieved by finding a matrix of that function (there always is one), and then performing simple matrix-vector multiplication.

Let $f'(\mathbf{x})$ be the matrix of the linear function $\mathbf{df}(\mathbf{x})$. Then, for a sufficiently small-enough perturbation $\mathbf{h}$, the linear approximation becomes

$$
f(\mathbf{x}+\mathbf{h})\approx f(\mathbf{x})+ \left(\mathbf{df}(\mathbf{x})\right)(\mathbf{h})=f(\mathbf{x})+f'(\mathbf{x})\mathbf{h}
$$

We call the matrix the Jacobian matrix, and use $J_{\mathbf{x}}\equiv f'(\mathbf{x})\in\mathbb{R}^{m\times n}$ to represent this quantity. Note that the shape is the same as we expect for matrices operating on $n$-dimensional column-space and $m$-dimensional row-space.

With Jacobian, we obtain a simplified evaluation rule for our approximation similar to the scalar-case, as $J_{\mathbf{x}}\mathbf{h}$ is simple matrix-vector multiplication.

### Scalar-valued Functions on Hilbert Spaces: Gradient Vector
Let's consider scalar-valued functions $f:U\to\mathbb{R}$ (or $\mathbb{C}$) (called functionals) on complete inner-product spaces $U$ (Hilbert space). For derivatives of such cases, we can use another trick. For any bounded linear functional $L:U\to\mathbb{R}$, there exists a unique vector $\boldsymbol{\varphi}_L$ that achieves the same effect with a simple inner product (Riesz Representation Theorem), i.e., $L(\mathbf{h})=\langle \boldsymbol{\varphi}_L, \mathbf{h}\rangle$. 

For the derivative, we use a special notation $\nabla$ to define this vector, such that 

$$
\nabla_\mathbf{x} f=\boldsymbol{\varphi}_{ L_{\mathbf{x}} }
$$ 

and write

$$
(\mathbf{df}(\mathbf{x}))(\mathbf{h})=\langle \nabla_\mathbf{x} f, \mathbf{h}\rangle
$$

For functions $f:\mathbb{R}^n\to\mathbb{R}$, this equals to the transpose of the Jacobian (as $J_\mathbf{x}$ is the row vector $\mathbb{R}^{1\times n}$)

$$
\nabla_\mathbf{x} f=J_\mathbf{x}^\top
$$

Replacing the inner-product by its finite-dimensional variant, the dot-product, we simplify

$$
f(\mathbf{x}+\mathbf{h})\approx f(\mathbf{x})+f'(\mathbf{x})\mathbf{h}=f(\mathbf{x})+\nabla_\mathbf{x} f\cdot\mathbf{h}
$$

### Derivatives of Matrix-Functions: Jacobian Tensor & Gradient Matrix
The benefit of Fréchet differentiability is that we can extend the notion of derivatives easily to functions with any normed-vector field domains. 

For functions defined on matrices $f:\mathbb{R}^{m\times n}\to\mathbb{R}^k$, the Jacobian $J_\mathbf{x}$ is simply the tensor of dimension $\mathbb{R}^{k\times m\times n}$. 

For real-valued functions $f:\mathbb{R}^{m\times n}\to\mathbb{R}$, the gradient is the matrix $\nabla_\mathbf{x} f\in \mathbb{R}^{m\times n}$ (since the first dimension of the Jacobian tensor is $1$)

### Functions with Bounded Derivative: Lipschitz Functions
Now, let's revisit the original promise of derivatives as discussed in the first section. We keep the context of functions on general normed-vector spaces $f:U\to V$. One of the ways we recognise "well-behaved" functions is by the derivatives being bounded. The notion we discuss here is Lipschitz continuity.

Typically, Lipschitz continuity is defined using the norm-view of the function. To define this clearly, let's use $\Vert\cdot\Vert_U$ to define the norm on the input space $U$, and similarly for $V$. We call the function L-Lipschitz as long as for every pair of input points $\mathbf{x}$ and $\mathbf{y}$, we can find a $L\geq 0$ such that the change in output is bounded by change in input, up to a multiplicative factor of $L$, i.e.,

$$
\Vert f(\mathbf{x})-f(\mathbf{y})\Vert_V\leq L\Vert\mathbf{x}-\mathbf{y}\Vert_U
$$

We can equivalently define this via the norm of the differential operator. Intuitively, this norm (like every operator norm) captures the "blow-up" factor of this operator:

$$
\Vert\mathbf{df}_\mathbf{x}\Vert_{\text{op}}:=\sup\limits_{\mathbf{h}\in U; \mathbf{h}\neq \mathbf{0}}\frac{\Vert\mathbf{df}_\mathbf{x}(\mathbf{h})\Vert_V}{\Vert\mathbf{h}\Vert_U}
$$

Under this definition, a bounded operator norm for the differential for the entire domain is a necessary and sufficient condition for the function being L-Lipschitz.

$$
\sup\limits_{\mathbf{x}\in U}\Vert\mathbf{df}_\mathbf{x}\Vert_{\text{op}}\leq L 
$$

For Euclidean spaces, this simply means that the Jacobian's largest Eigenvalue (i.e., the spectral norm of the Jacobian matrix) is bounded by $L$.

### Operator View of the Gradient
### The Total Derivative Theorem
### Symmetry of Second Derivatives: Clairaut's Theorem
### Taylor's Theorem & The Hessian

## Integration
### Notation & Hyper-volume Elements
### Integrals as Linear Functionals
### Multiple Integrals & Order Swapping (Fubini's Theorem)
### Leibniz Integral Rule (Differentiating Under the Integral Sign)
### Change of Variables: Pushing Back Local Volume
### Integration by Parts & Divergence: The Adjoint Perspective
