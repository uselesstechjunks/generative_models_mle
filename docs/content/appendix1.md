# Just Enough Calculus

## 1. Differentiation
Given a function, a useful question regarding its nature is: what happens to the output when we poke the input slightly. More formally, considering additive perturbations $x\mapsto x+h$, we ask by how it make the output move: $f(x)\mapsto f(x+h)$. 

The goal often is: if a function is "nice" (doesn't fluctuate drastically; i.e., we have some bound on how much it fluctuates for small-enough perturbations), we can use it in certain cases that otherwise would be impossible.

### 1.1 Scalar Functions
As you might recall, for scalar-valued functions on scalar domains $f:\mathbb{R}\to\mathbb{R}$, this is typically introduced as a ratio (since it's possible to compute ratios with scalars) and passing the limit of the perturbation to 0. When this limit exists, we define

$$
f'(x):=\lim\limits_{h\to 0}\frac{f(x+h)-f(x)}{h} \left[\equiv\frac{\mathop{df}}{\mathop{dx}}\right].
$$

With this quantity, the changed output under any perturbations $h$ can be approximated by performing a simple multiplication $f'(x)h$, followed by an addition. This approximation is "decent" when $h$ is small. That is, we claim, without re-evaluating the function at $x+h$, that:

$$
f(x+h)\approx f(x)+f'(x)h
$$

To see why this approximation makes sense, rewriting the definition by subtracting $f'(x)$ from both sides and pulling it in inside the ratio helps:

$$
\lim\limits_{h\to 0}\frac{f(x+h)-f(x)-f'(x)h}{h}=0
$$

We can stop here. But let's take it one step further. The above is equivalent to saying that if we consider the error (say, $\epsilon$) in our approximation from whichever direction (positive or negative) as a dangling term in the numerator

$$
\frac{f(x+h)-f(x)-f'(x)h-\vert\epsilon\vert}{h}
$$

then 

$$
\lim\limits_{h\to 0} \frac{\vert\epsilon\vert}{h}=0.
$$

Why bother? Here's why: unlike the scalar-case, for functions involving general vector spaces, ratios are not defined. But, as we discuss in the following section, this new angle connects it to how differentiability is defined in such cases.

### 1.2 General Normed Vector-Spaces
Let's consider functions of the form $f:\mathcal{U}\to \mathcal{V}$, where $\mathcal{U}$ and $\mathcal{V}$ are arbitrary normed vector spaces (see Just Enough Linear Algebra). The change in the output under a perturbation $\mathbf{h}\in \mathcal{U}$ is the vector $\Delta\mathbf{f}\in\mathcal{V}:=f(\mathbf{x}+\mathbf{h})-f(\mathbf{x})$, that depends on the $\mathbf{h}$ as well as the point $\mathbf{x}$ that we pin it on.

#### 1.2.1 Fréchet Differentiability
The influence of $\mathbf{h}$ on the output can be understood by breaking $\Delta\mathbf{f}$ down into 2 parts that stays valid regardless of $\mathbf{h}$ - a part that changes linearly with $\mathbf{h}$, and another part that captures all the leftover non-linear influences:

$$
\Delta\mathbf{f}=\underbrace{L_\mathbf{x}(\mathbf{h})}_ {\text{linear}}+\underbrace{E_\mathbf{x}(\mathbf{h})}_{\text{non-linear}}
$$

(I used subscript for $\mathbf{x}$ and left $\mathbf{h}$ as a parameter since $\mathbf{x}$ - the evaluation-point - is fixed. We vary only the perturbation $\mathbf{h}$.)

The motivation here is: if the non-linear part is negligible, we can ignore it and use the linear part as our desired approximation of $\Delta\mathbf{f}$. Under this framing, $E_\mathbf{x}(\mathbf{h})$ represents the "error" in our approximation.

To bound this error, similar to the ratio $\vert\epsilon\vert/h$ we discussed in the scalar case, we consider the ratio of the norms (possible since norms produce reals). 

To define this cleanly, let's use $\Vert\cdot\Vert_\mathcal{U}$ for the norm on the input space $\mathcal{U}$, and similarly $\Vert\cdot\Vert_\mathcal{V}$ for $\mathcal{V}$. 

As we reduce the magnitude of the perturbation, if the magnitude of the error-term reduces faster (i.e., their ratio vanishes in the limit), 

$$
\lim\limits_{\mathbf{h}\to\mathbf{0}} \frac{\Vert E_\mathbf{x}(\mathbf{h}) \Vert_\mathcal{V}}{\Vert \mathbf{h}\Vert_\mathcal{U}}= 0,
$$

then we consider the error to be negligible for small-enough $\mathbf{h}$. We use the small-o notation $E_\mathbf{x}(\mathbf{h})=o(\Vert\mathbf{h}\Vert)$ to capture this, and we consider the function to be "differentiable". 

##### Uniqueness
Note that we didn't rely on a specific $L_\mathbf{x}$ for our decomposition to be valid. For any $L_\mathbf{x}$ we pick, one can find a corresponding $E_\mathbf{x}$. Clearly, the ratio doesn't vanish in the limit for any arbitrary choice of $L_\mathbf{x}$. There must be something special about the $L_\mathbf{x}$ that achieves that. A question one might ask: does special necessarily mean unique. The answer is yes. See Appendix 1 for a convincing argument.

Let's call the set of all bounded (why bounded?) linear maps $\mathcal{L}(\mathcal{U},V)$. Assuming $f$ is differentiable, a specific (why specific?) $D_{\mathbf{x}}\in\mathcal{L}$ makes the error negligible in limit. We call this unique $D_{\mathbf{x}}$ the derivative of the function $f$ at $\mathbf{x}$.

Note that the derivative has the same domain and co-domain as $f$, i.e., $D_{\mathbf{x}}:\mathcal{U}\to V$. It is linear by definition, and it produces $D_{\mathbf{x}}(\mathbf{h})\in \mathcal{V}$ for every $\mathbf{h}\in \mathcal{U}$, so that the following equality (note, equality) holds:

$$
f(\mathbf{x}+\mathbf{h})=f(\mathbf{x})+D_{\mathbf{x}}(\mathbf{h})+o(\Vert\mathbf{h}\Vert)
$$

$f(\mathbf{x})+D_{\mathbf{x}}(\mathbf{h})$ only becomes a "good-enough" approximation of $f(\mathbf{x}+\mathbf{h})$ as $\mathbf{h}\to\mathbf{0}$.

#### 1.2.2 Differential Operator
Since the derivative $D_{\mathbf{x}}$ depends on $\mathbf{x}$, we can identify an operator, $Df:\mathbf{x}\mapsto D_{\mathbf{x}}$, that produces this derivative linear map for every $\mathbf{x}$ in domain. This is the differential operator, $Df:\mathcal{U}\to\mathcal{L}(\mathcal{U},\mathcal{V})$. Using this notation, the approximation for small $\mathbf{h}$ becomes

$$
f(\mathbf{x}+\mathbf{h})\approx f(\mathbf{x})+D_{\mathbf{x}}(\mathbf{h})=f(\mathbf{x})+ \left(Df(\mathbf{x})\right)(\mathbf{h})
$$

I've used the functional notation over the traditional one ($Df(\mathbf{x})[\mathbf{h}]$) for better readability.

#### 1.2.3 Gateaux Differentiability


### 1.4 Special Cases
Jacobians and Gradients are typically discussed in Euclidean space, and are defined in terms of their components. In the following, we revisit them from Fréchet differentiability perspective which, in my opinion, provides useful insights on extending these ideas to more complex cases.

#### 1.4.1 Euclidean Vector-Spaces: Jacobian
For functions involving Euclidean spaces (e.g., $f:\mathbb{R}^n\to\mathbb{R}^m$), we can use a trick. In finite dimension, the effect of applying any linear map can be achieved by finding a matrix of that transformation (there always is one - why?), and then performing a matrix-vector multiplication.

Let $f'(\mathbf{x})\in\mathbb{R}^{m\times n}$ be the matrix of the linear map $Df(\mathbf{x})$. Then, for a small-enough perturbation $\mathbf{h}$, the linear approximation becomes

$$
f(\mathbf{x}+\mathbf{h})\approx f(\mathbf{x})+ \left(Df(\mathbf{x})\right)(\mathbf{h})=f(\mathbf{x})+f'(\mathbf{x})\mathbf{h}
$$

We call the matrix the Jacobian matrix, and use $J_{\mathbf{x}}\equiv f'(\mathbf{x})$ to represent this quantity. With this, we obtain a simplified evaluation rule for our approximation similar to the scalar-case, as $J_{\mathbf{x}}\mathbf{h}$ is a simple matrix-vector multiplication.

#### 1.4.2 Scalar-valued Functions on Hilbert Spaces: Gradient Vector
Let's consider scalar-valued functions $f:\mathcal{H}\to\mathbb{R}$ on complete inner-product spaces $\mathcal{H}$ (Hilbert space). We can use another trick for derivatives here. For every $L\in\mathcal{L}(\mathcal{H}, \mathbf{R})$, we'd find a unique vector $\boldsymbol{\varphi}_L\in\mathcal{H}$ that achieves the same effect as applying the function with a simple inner product instead (Riesz Representation Theorem - why does this hold?), i.e., $L(\mathbf{h})=\langle \boldsymbol{\varphi}_L, \mathbf{h}\rangle$.

For the derivative $D_\mathbf{x}\in\mathcal{L}$, we use a special notation $\nabla_\mathbf{x} f=\boldsymbol{\varphi}_ {D_{\mathbf{x}}}$ to denote this vector, and write

$$
(Df(\mathbf{x}))(\mathbf{h})=\langle \nabla_\mathbf{x} f, \mathbf{h}\rangle
$$

Now, back to functions on Euclidean domains $f:\mathbb{R}^n\to\mathbb{R}$, this equals to the transpose of the Jacobian (as $J_\mathbf{x}$ is the row vector $\mathbb{R}^{1\times n}$)

$$
\nabla_\mathbf{x} f=J_\mathbf{x}^\top
$$

Replacing the inner-product by its finite-dimensional counterpart, the dot-product, we simplify our approximation rule:

$$
f(\mathbf{x}+\mathbf{h})\approx f(\mathbf{x})+f'(\mathbf{x})\mathbf{h}=f(\mathbf{x})+\nabla_\mathbf{x} f\cdot\mathbf{h}
$$

### 1.5 More Special Cases
The sophisticated machinery for differentiability a la Fréchet pays off as it allows us to extend derivatives to functions on any normed-vector space, as we discuss in the following section.

#### 1.5.1 Derivatives of Matrix-Functions: Jacobian Tensor & Gradient Matrix
Recall that the space of matrices is a vector space on its own right, and the fact that matrix norms exist. For functions defined on matrices $f:\mathbb{R}^{m\times n}\to\mathbb{R}^k$, the Jacobian $J_\mathbf{x}$ is the tensor of dimension $\mathbb{R}^{k\times m\times n}$. 

For real-valued functions $f:\mathbb{R}^{m\times n}\to\mathbb{R}$, the gradient is the matrix $\nabla_\mathbf{x} f\in \mathbb{R}^{m\times n}$ (since the first dimension of the Jacobian tensor is $1$)

#### 1.5.2 Gradient of a Functional involving Probability Densities
This section contains an example that is particularly insightful for transport problem and Langevin dynamics.

### 1.6 Functions with Bounded Derivative: Lipschitz Functions
Now, let's revisit the original promise of derivatives as discussed in the first section. We keep the context of functions on general normed-vector spaces $f:U\to V$. One of the ways we recognise "well-behaved" functions is by the derivatives having a specific upper bound. This notion is called Lipschitz continuity.

Typically, Lipschitz continuity is defined using the norm-view of the function. We call the function L-Lipschitz as long as we can find an $L\geq 0$ such that for every pair of input points $\mathbf{x}$ and $\mathbf{y}$, the change in the output is bounded by change in the input, up to a multiplicative factor of $L$, i.e.,

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

# Appendix
## 1. Uniqueness of Fréchet Derivative
Let's consider another candidate for the derivative at $\mathbf{x}$, $L'_ \mathbf{x}$ (and its corresponding $E'_ \mathbf{x}$) and see if we can convince ourselves that $L_ \mathbf{x}=L'_ \mathbf{x}$. 

We first do some algebra using the decomposition $E_ \mathbf{x}(\mathbf{h})=\Delta\mathbf{f} - L_\mathbf{x}(\mathbf{h})$:

$$
\frac{\Vert E_\mathbf{x}(\mathbf{h})-E'_\mathbf{x}(\mathbf{h})\Vert_\mathcal{V}}{\Vert\mathbf{h}\Vert_\mathcal{U}}=\frac{\Vert \left(\Delta\mathbf{f} - L_\mathbf{x}(\mathbf{h})\right) -\left(\Delta\mathbf{f} - L'_\mathbf{x}(\mathbf{h})\right)\Vert_\mathcal{V}}{\Vert\mathbf{h}\Vert_\mathcal{U}}=\frac{\Vert L'_\mathbf{x}(\mathbf{h})-L_\mathbf{x}(\mathbf{h})\Vert_\mathcal{V}}{\Vert\mathbf{h}\Vert_\mathcal{U}}
$$

The numerator we get on the right is itself a linear map.

$$

$$
