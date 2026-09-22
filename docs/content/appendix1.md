# Just Enough Calculus

## 1. Differentiation
Given a function, a useful inquiry regarding its nature is: what happens to the output of the function when we perturb the input slightly. Concretely, considering additive perturbations, $x\mapsto x+\delta$, we check how much it affects the output, $f(x)\mapsto f(x+\delta)$. The goal here is: assuming that the function doesn't fluctuate drastically (i.e., we have some bound on how much it deviates for small-enough changes in the input), we can establish certain properties of the functions that makes it possible to use these functions in cases that otherwise would be impossible.

### 1.1 Scalar Functions
For scalar-valued functions on scalar domains $f:\mathbb{R}\to\mathbb{R}$ this is quantified by introducing a ratio (since it's possible to compute ratios with scalars) and pushing its limit to infinitesimal perturbations. When this limit exists, we define

$$
f'(x)\equiv\mathop{\frac{d}{dx}}f:=\lim\limits_{\delta\to 0}\frac{f(x+\delta)-f(x)}{\delta}
$$

With this quantity, the changed output under "small-enough" perturbations $h$ can be approximated well by performing a simple multiplication $f'(x)h$, followed by a simple addition. That is, we can claim, without having to re-evaluate the function at $x+h$, that:

$$
f(x+h)\approx f(x)+f'(x)h
$$

For functions in general vector spaces, ratios are not defined. Fréchet derivative captures this notion with a slightly different machinery.

### 1.2 General Normed Vector-Spaces
Let's assume that we have a function $f:U\to V$, where $U$ and $V$ are arbitrary vector spaces with a norm (i.e., we can compute length of vectors in these spaces). The change in the output space is the vector, $\delta\mathbf{f}:=f(\mathbf{x}+\boldsymbol{\delta})-f(\mathbf{x})$, that depends on the perturbation $\boldsymbol{\delta}\in U$ as well as the point we evaluate it on (i.e., $\mathbf{x}\in U$). Note that $\delta\mathbf{f}\in V$.

#### 1.2.1 Fréchet Differentiability
The change vector can be decomposed of 2 parts - a part that changes linearly with $\boldsymbol{\delta}$, and another that captures all the non-linear influences:

$$
\delta\mathbf{f}=\underbrace{L_{\mathbf{x}}(\boldsymbol{\delta})}_{\text{linear}}+\underbrace{E_{\mathbf{x}}(\boldsymbol{\delta})}_{\text{non-linear}}
$$

I used subscript for $\mathbf{x}$ and kept $\boldsymbol{\delta}$ as a parameter since $\mathbf{x}$ - the evaluation-point - is constant here, as we vary the perturbation $\boldsymbol{\delta}$.

The motivation behind this decomposition is this: if the non-linear part is negligible, we can ignore it and use the linear part as our desired approximation of the change vector $\delta\mathbf{f}$. Under this framing, $E_{\mathbf{x}}(\boldsymbol{\delta})$ represents the "error" in our approximation.

To bound this error, we introduce the ratio of the norms, i.e., $\frac{\Vert E_{\mathbf{x}}(\boldsymbol{\delta}) \Vert}{\Vert \boldsymbol{\delta}\Vert}$ (possible since norms produce reals). As we reduce the magnitude of the perturbation, if the magnitude of the error reduces faster (i.e., their ratio vanishes in the limit), 

$$
\lim\limits_{\boldsymbol{\delta}\to 0} \frac{\Vert E_{\mathbf{x}}(\boldsymbol{\delta}) \Vert}{\Vert \boldsymbol{\delta}\Vert}= 0,
$$

then we consider the error to be negligible for small-enough $\boldsymbol{\delta}$. We use the small-oh notation for this error, i.e., $E_{\mathbf{x}}(\boldsymbol{\delta})=o(\Vert\boldsymbol{\delta}\Vert)$ to capture this, and we consider the function to be "differentiable". 

Clearly, this would not hold for any arbitrary choice of linear function $L_\mathbf{x}$. Let's call the set of all bounded (why bounded?) linear functions $\mathcal{L}(U,V)$. Assuming $f$ is differentiable, a specific (why specific?) $D_{\mathbf{x}}\in\mathcal{L}$ makes the error $0$ in limit. We call this unique $D_{\mathbf{x}}$ the derivative of the function $f$ at $\mathbf{x}$.

Note that the derivative is a function that has the same domain and co-domain as $f$, i.e., $D_{\mathbf{x}}:U\to V$. It is linear by definition, and it produces $D_{\mathbf{x}}(\mathbf{h})\in V$ for every $\mathbf{h}\in U$, so that the following equality (note, equality) holds:

$$
f(\mathbf{x}+\mathbf{h})=f(\mathbf{x})+D_{\mathbf{x}}(\mathbf{h})+o(\Vert\mathbf{h}\Vert)
$$

$f(\mathbf{x})+D_{\mathbf{x}}(\mathbf{h})$ only becomes a "good-enough" approximation of $f(\mathbf{x}+\mathbf{h})$ when $\Vert\mathbf{h}\Vert\to 0$.

### 1.2.2 Differential Operator
Since the derivative $D_{\mathbf{x}}$ depends on $\mathbf{x}$, we can identify an operator, $Df:\mathbf{x}\mapsto D_{\mathbf{x}}$, that produces this derivative function for every $\mathbf{x}$ in domain. This is the differential operator, $Df:U\to\mathcal{L}(U,V)$. Using this notation, the approximation for small $\mathbf{h}$ becomes

$$
f(\mathbf{x}+\mathbf{h})\approx f(\mathbf{x})+D_{\mathbf{x}}(\mathbf{h})=f(\mathbf{x})+ \left(Df(\mathbf{x})\right)(\mathbf{h})
$$

### 1.4 Special Cases
Jacobians and Gradients are typically discussed in Euclidean space, and are defined in terms of their components. In the following, we revisit them from Fréchet differentiability perspective which, in my opinion, provides useful insights on extending these ideas to more complex cases.

#### 1.4.1 Euclidean Vector-Spaces: Jacobian
For functions involving Euclidean spaces (e.g., $f:\mathbb{R}^n\to\mathbb{R}^m$), we can use a trick. In finite dimension, the effect of applying any linear function can be achieved by finding a matrix of that transformation (there always is one - why?), and then performing a matrix-vector multiplication.

Let $f'(\mathbf{x})\in\mathbb{R}^{m\times n}$ be the matrix of the linear function $Df(\mathbf{x})$. Then, for a small-enough perturbation $\mathbf{h}$, the linear approximation becomes

$$
f(\mathbf{x}+\mathbf{h})\approx f(\mathbf{x})+ \left(Df(\mathbf{x})\right)(\mathbf{h})=f(\mathbf{x})+f'(\mathbf{x})\mathbf{h}
$$

We call the matrix the Jacobian matrix, and use $J_{\mathbf{x}}\equiv f'(\mathbf{x})$ to represent this quantity. With this, we obtain a simplified evaluation rule for our approximation similar to the scalar-case, as $J_{\mathbf{x}}\mathbf{h}$ is a simple matrix-vector multiplication.

#### 1.4.2 Scalar-valued Functions on Hilbert Spaces: Gradient Vector
Let's consider scalar-valued functions $f:U\to\mathbb{R}$ on inner-product spaces $U$. As long as the space is complete under this inner-product (Hilbert space), we can use another trick for derivatives of such cases. For any bounded real-valued linear function $L\in\mathcal{L}(U, \mathbf{R})$, there exists a unique vector $\boldsymbol{\varphi}_L\in U$ that achieves the effect of applying the function with a simple inner product (Riesz Representation Theorem - why does this hold?), i.e., $L(\mathbf{h})=\langle \boldsymbol{\varphi}_L, \mathbf{h}\rangle$.

For the derivative $D_\mathbf{x}\in\mathcal{L}$, we use a special notation $\nabla$ to define this vector, $\nabla_\mathbf{x} f=\boldsymbol{\varphi}_ {D_{\mathbf{x}}}$, and write

$$
(Df(\mathbf{x}))(\mathbf{h})=\langle \nabla_\mathbf{x} f, \mathbf{h}\rangle
$$

Now, back to functions on Euclidean domains $f:\mathbb{R}^n\to\mathbb{R}$, this equals to the transpose of the Jacobian (as $J_\mathbf{x}$ is the row vector $\mathbb{R}^{1\times n}$)

$$
\nabla_\mathbf{x} f=J_\mathbf{x}^\top
$$

Replacing the inner-product by its finite-dimensional variant, the dot-product, we simplify our approximation rule:

$$
f(\mathbf{x}+\mathbf{h})\approx f(\mathbf{x})+f'(\mathbf{x})\mathbf{h}=f(\mathbf{x})+\nabla_\mathbf{x} f\cdot\mathbf{h}
$$

### 1.5 More Special Cases
The sophisticated machinery for differentiability a la Fréchet pays off as it allows us to extend derivatives to functions on any normed-vector space, as we discuss in the following two sections.

#### 1.5.1 Derivatives of Matrix-Functions: Jacobian Tensor & Gradient Matrix
Recall that the space of matrices is a vector space on its own right, and the fact that matrix norms exist. For functions defined on matrices $f:\mathbb{R}^{m\times n}\to\mathbb{R}^k$, the Jacobian $J_\mathbf{x}$ is the tensor of dimension $\mathbb{R}^{k\times m\times n}$. 

For real-valued functions $f:\mathbb{R}^{m\times n}\to\mathbb{R}$, the gradient is the matrix $\nabla_\mathbf{x} f\in \mathbb{R}^{m\times n}$ (since the first dimension of the Jacobian tensor is $1$)

#### 1.5.2 Gradient of a Functional over a Space of Distributions
TODO

### 1.6 Functions with Bounded Derivative: Lipschitz Functions
Now, let's revisit the original promise of derivatives as discussed in the first section. We keep the context of functions on general normed-vector spaces $f:U\to V$. One of the ways we recognise "well-behaved" functions is by the derivatives having a specific upper bound. This notion is called Lipschitz continuity.

Typically, Lipschitz continuity is defined using the norm-view of the function. To define this clearly, let's use $\Vert\cdot\Vert_U$ to define the norm on the input space $U$, and similarly for $V$. We call the function L-Lipschitz as long as we can find an $L\geq 0$ such that for every pair of input points $\mathbf{x}$ and $\mathbf{y}$, the change in the output is bounded by change in the input, up to a multiplicative factor of $L$, i.e.,

$$
\Vert f(\mathbf{x})-f(\mathbf{y})\Vert_V\leq L\Vert\mathbf{x}-\mathbf{y}\Vert_U
$$

We can equivalently define this by claiming that the norm of the differential operator has an upper bound of $L$. Intuitively, this norm (like every operator norm) captures the "blow-up" factor. To define the operator norm, we use the norm of the derivative function at any $\mathbf{x}$:

$$
\Vert Df(\mathbf{x})\Vert_\infty:=\sup\limits_{\mathbf{h}\in U; \mathbf{h}\neq \mathbf{0}}\frac{\Vert (Df(\mathbf{x}))(\mathbf{h})\Vert_V}{\Vert\mathbf{h}\Vert_U}
$$

The operator norm is defined to capture the maximum exploding factor by a derivative for any point in its domain:

$$
\Vert Df\Vert_{\text{op}}=\sup\limits_{\mathbf{x}\in U}\Vert Df(\mathbf{x})\Vert_\infty
$$

Under this definition, $\Vert Df\Vert_{\text{op}}\leq L$ is a necessary and sufficient condition for the function being L-Lipschitz.

For Euclidean spaces, this implies that the Jacobian's largest singular value (spectral norm) has upper bound $L$.

### 1.7 The Total Derivative Theorem
### 1.8 Symmetry of Second Derivatives: Clairaut's Theorem
### 1.9 Taylor's Theorem & The Hessian

## 2. Integration
### 2.1 Notation & Hyper-volume Elements
### 2.2 Integrals as Linear Functionals
### 2.3 Multiple Integrals & Order Swapping (Fubini's Theorem)
### 2.4 Leibniz Integral Rule (Differentiating Under the Integral Sign)
### 2.5 Change of Variables: Pushing Back Local Volume
### 2.6 Integration by Parts & Divergence: The Adjoint Perspective

## Operator View of the Gradient
