# Just Enough Calculus

## 1. Differentiation
Given a function, a useful question regarding its nature is: what happens to the output when we poke the input slightly. Formally, for additive perturbations $x\mapsto x+h$, we ask by how it makes the output fluctuate: $f(x)\mapsto f(x+h)$. 

The goal often is: if a function is "nice" (doesn't fluctuate drastically; i.e., we have some bound on how much it changes under small-enough perturbations), we can use it in certain cases to make things easy for us.

### 1.1 Scalar Functions
As you might recall, for scalar-valued functions on scalar domains $f:\mathbb{R}\to\mathbb{R}$, this is typically defined with a ratio (since it's possible to compute ratios with scalars) and passing the limit of the perturbation to 0. When this limit exists, we define it as the derivative of $f$ at $x$

$$
f'(x):=\lim\limits_{h\to 0}\frac{f(x+h)-f(x)}{h} \left[\equiv\frac{\mathop{df}}{\mathop{dx}}\right].
$$

The changed output under any perturbations $h$ can be approximated by scaling it up with $f'(x)$, and then adding that to the unperturbed function value $f(x)$. That is, we claim, without re-evaluating the function at $x+h$, that:

$$
f(x+h)\approx f(x)+f'(x)h
$$

This approximation is "decent" when $h$ is small. To see why, rewriting the definition by subtracting $f'(x)$ from both sides and pulling it in inside the ratio makes it pop up at the numerator:

$$
\lim\limits_{h\to 0}\frac{f(x+h)-f(x)-f'(x)h}{h}=0
$$

We can stop here. But let's take it one step further. The above is equivalent to saying that if we kept the error in our approximation (say, $\epsilon$) from whichever direction (positive or negative) as a dangling term in the numerator

$$
\frac{f(x+h)-f(x)-f'(x)h-\vert\epsilon\vert}{h}
$$

then it must be the case that

$$
\lim\limits_{h\to 0} \frac{\vert\epsilon\vert}{h}=0.
$$

Why bother with this? Unlike the scalar-case, for functions involving general vector spaces, ratios are not defined. But, as we discuss in the following section, this equivalence connects it to how differentiability is defined in such cases.

### 1.2 General Normed Vector-Spaces
Let's consider functions of the form $f:\mathcal{U}\to \mathcal{V}$, where $\mathcal{U}$ and $\mathcal{V}$ are arbitrary normed vector spaces (see Just Enough Linear Algebra). The change in the output under a perturbation $\mathbf{h}\in \mathcal{U}$ is the vector $\Delta\mathbf{f}\in\mathcal{V}:=f(\mathbf{x}+\mathbf{h})-f(\mathbf{x})$. It depends on the $\mathbf{h}$ as well $\mathbf{x}$.

#### 1.2.1 Fréchet Differentiability
The influence of $\mathbf{h}$ on the output can be analysed by breaking $\Delta\mathbf{f}$ down into 2 parts that stays valid regardless of $\mathbf{h}$ - a part that scales linearly with $\mathbf{h}$, and another part that captures all the leftover non-linear influences:

$$
\Delta\mathbf{f}=\underbrace{L_\mathbf{x}(\mathbf{h})}_ {\text{linear}}+\underbrace{E_\mathbf{x}(\mathbf{h})}_{\text{non-linear}}
$$

Aside: I used subscript for $\mathbf{x}$ and left $\mathbf{h}$ as a parameter since $\mathbf{x}$ - the evaluation-point - is fixed. We're changing only the perturbation $\mathbf{h}$.

The motivation here is: if the non-linear part is negligible, we can ignore it and use the linear part as our desired approximation of $\Delta\mathbf{f}$. Under this framing, $E_\mathbf{x}(\mathbf{h})$ represents the "error" in our approximation.

To bound this error, similar to the error-ratio we discussed in the scalar case, we consider the ratio of the norms (possible since norms produce reals). 

To define this cleanly, let's use $\Vert\cdot\Vert_\mathcal{U}$ for the norm on the input space $\mathcal{U}$, and similarly $\Vert\cdot\Vert_\mathcal{V}$ for $\mathcal{V}$. 

As we reduce the magnitude of the perturbation, if the magnitude of the error-term reduces faster, then their ratio vanishes in the limit:

$$
\lim\limits_{\mathbf{h}\to\mathbf{0}} \frac{\Vert E_\mathbf{x}(\mathbf{h}) \Vert_\mathcal{V}}{\Vert \mathbf{h}\Vert_\mathcal{U}}= 0,
$$

That is, we can consider the error to be negligible for small-enough $\mathbf{h}$. We use the small-o notation $E_\mathbf{x}(\mathbf{h})=o(\Vert\mathbf{h}\Vert)$ to capture this, and we declare the function to be "differentiable". 

Note that we didn't rely on a specific $L_\mathbf{x}$ for our decomposition to be valid: for any $L_\mathbf{x}$ we pick, one can find a corresponding $E_\mathbf{x}$. Clearly, the ratio doesn't vanish in the limit for any arbitrary choice of $L_\mathbf{x}$. There must be something special about the $L_\mathbf{x}$ that achieves that. A question one might ask: does special necessarily mean unique. The answer is yes. See Appendix 1 for a convincing argument.

As it's unique, it helps to denote it with a special symbol $L^\ast_\mathbf{x}$. We call it the derivative of $f$ at $\mathbf{x}$.

Note that the derivative is a function (map) itself with the same domain and co-domain as $f$, i.e., $L^\ast_\mathbf{x}:\mathcal{U}\to V$. It is linear by definition, and it outputs vectors $L^\ast_\mathbf{x}(\mathbf{h})$ in $\mathcal{V}$ assuring that the following equality holds for every $\mathbf{h}$:

$$
f(\mathbf{x}+\mathbf{h})=f(\mathbf{x})+L^\ast_\mathbf{x}(\mathbf{h})+o(\Vert\mathbf{h}\Vert)
$$

#### 1.2.2 Differential Operator
Since the derivative depends on $\mathbf{x}$, we need a way to define it for every $\mathbf{x}$. This is done by introducing an operator $Df:\mathbf{x}\mapsto L^\ast_\mathbf{x}$. It is called the differential operator (or the "derivative-map") and has the shape $Df:\mathcal{U}\to(\mathcal{U}\to\mathcal{V})$.

Using the operator notation, the approximation for small $\mathbf{h}$ looks as follows:

$$
f(\mathbf{x}+\mathbf{h})\approx f(\mathbf{x})+D_{\mathbf{x}}(\mathbf{h})=f(\mathbf{x})+ \left(Df(\mathbf{x})\right)(\mathbf{h})
$$

I've used the functional notation over the traditional $Df(\mathbf{x})[\mathbf{h}]$ for better readability.

### 1.4 Special Cases
When we learn about Jacobians and Gradients, they are typically presented in the context of Euclidean spaces (i.e., $\mathbb{R}^d$) and are described in terms of their components. In the following, let's revisit them from Fréchet differentiability perspective. In my opinion, this should help us appreciate the connection as we extend these ideas to more complex cases.

#### 1.4.1 Euclidean Vector-Spaces: Jacobian
For functions such as $f:\mathbb{R}^n\to\mathbb{R}^m$, we can use a trick for the derivative. In finite dimensions, the effect of applying any linear-map on a vector can be achieved by first finding a matrix of that map, and then multiplying the vector with that matrix. Once we choose our base, it is guaranteed that there always is a matrix for every linear-map (see Just Enough Linear Algebra).

Let's use $f'(\mathbf{x})\in\mathbb{R}^{m\times n}$ for the matrix corresponding to $Df(\mathbf{x})$ for the usual choice of base (along the co-ordinate axes). Then, for a small-enough $\mathbf{h}$, the linear approximation becomes

$$
f(\mathbf{x}+\mathbf{h})\approx f(\mathbf{x})+ \left(Df(\mathbf{x})\right)(\mathbf{h})=f(\mathbf{x})+f'(\mathbf{x})\mathbf{h}
$$

With this, we get an evaluation rule similar to the scalar-case. We call the matrix the Jacobian matrix, and use $J_{\mathbf{x}}$ for it.

#### 1.4.2 Scalar-valued Functions on Hilbert Spaces: Gradient Vector
Gradients are much more interesting than they appear at a first glance. To see why, let's consider scalar-valued functions $f:\mathcal{H}\to\mathbb{R}$ on complete inner-product spaces $\mathcal{H}$ (see Just Enough Linear Algebra). 

Here, we can use another trick for the derivatives. For every linear-map $L:\mathcal{H}\to\mathbf{R}$, we'd find a unique vector $\boldsymbol{\varphi}_L$ occupying the same input space $\mathcal{H}$ that achieves the same effect as applying $L$ with a simple inner product instead, i.e., $L(\mathbf{h})=\langle \boldsymbol{\varphi}_L, \mathbf{h}\rangle _{\mathcal{H}}$ (Riesz Representation Theorem. See Just Enough Linear Algebra).

For the derivative of $f$ at $\mathbf{x}$, we reserve a special notation $\nabla_\mathbf{x} f$ instead of $\varphi$ for this vector, so that we can write

$$
(Df(\mathbf{x}))(\mathbf{h})=\langle \nabla_\mathbf{x} f, \mathbf{h}\rangle _{\mathcal{H}}
$$

Now, moving our focus back to functions on Euclidean domains $f:\mathbb{R}^n\to\mathbb{R}$, this happens to be equal to the transpose of the Jacobian component-by-component to make the algebra work (as $J_\mathbf{x}$ is the row matrix $\mathbb{R}^{1\times n}$):

$$
\nabla_\mathbf{x} f=J_\mathbf{x}^\top
$$

Replacing the inner-product by its finite-dimensional counterpart, the dot-product, we rewrite our approximation rule:

$$
f(\mathbf{x}+\mathbf{h})\approx f(\mathbf{x})+f'(\mathbf{x})\mathbf{h}=f(\mathbf{x})+\nabla_\mathbf{x} f\cdot\mathbf{h}
$$

### 1.5 More Special Cases
The sophisticated machinery for differentiability a la Fréchet pays off as it allows us to extend derivatives to functions on any normed space. We look at couple of interesting ones in this section.

#### 1.5.1 Derivatives of Matrix-Functions: Jacobian Tensor & Gradient Matrix
Recall that the space of matrices is a vector space on its own right, and the fact that matrix norms exist. For functions defined on matrices $f:\mathbb{R}^{m\times n}\to\mathbb{R}^k$, all of the discussion around derivatives work. The only change is in the dimensions involved:

- The Jacobian $J_\mathbf{x}$ is the tensor of dimension $\mathbb{R}^{k\times m\times n}$ (output dimension always is the first dimension).
- For $f:\mathbb{R}^{m\times n}\to\mathbb{R}$, we also have the gradient but as the matrix $\nabla_\mathbf{x} f\in \mathbb{R}^{m\times n}$ (since the first dimension of the Jacobian is $1$)

#### 1.5.2 Gradient of a Functional involving Probability Densities
In this section, we consider an example that is particularly relevant for the transport problem.

TODO

### 1.6 Functions with Bounded Derivative: Lipschitz Functions
Let's revisit the original promise of derivatives as discussed in the first section - helping us finding "nice" functions. We keep the context on general normed spaces. 

One of the ways we recognise well-behaved functions is by passing multiple inputs through it and putting bounds on how far apart they are allowed to land from one another. Lipschitz continuity captures this formally with distances via the norm.

We call a function L-Lipschitz as long as we can find an $L\geq 0$ such that any input pair $\mathbf{x},\mathbf{y}$ is able to bound the distance between their images by their own distance, up to a multiplicative factor of $L$, i.e.,

$$
\Vert f(\mathbf{x})-f(\mathbf{y})\Vert_\mathcal{V}\leq L\Vert\mathbf{x}-\mathbf{y}\Vert_\mathcal{U}
$$

This should be connected to differentiability in some way as the pair can be arbitrary close to one another. We formalise this by defining a norm of the differential operator and putting $L$ as an upper bound on it. Intuitively, this norm (like every operator norm) should capture the "blow-up" factor on its input.

To define the operator norm, we first use the fact that derivative at any $\mathbf{x}$ is just a linear-map and its own norm represents the blow-up factor for any $\mathbf{h}$:

$$
\Vert Df(\mathbf{x})\Vert_\infty:=\sup\limits_{\mathbf{h}\in \mathcal{U}; \mathbf{h}\neq \mathbf{0}}\frac{\Vert (Df(\mathbf{x}))(\mathbf{h})\Vert_\mathcal{V}}{\Vert\mathbf{h}\Vert_\mathcal{U}}
$$

For Euclidean space, this is simply the largest singular value of the Jacobian matrix.

The operator norm then captures the maximum blow-up factor of the derivatives across the entire domain:

$$
\Vert Df\Vert_{\text{op}}=\sup\limits_{\mathbf{x}\in\mathcal{U}}\Vert Df(\mathbf{x})\Vert_\infty
$$

Under this definition, $\Vert Df\Vert_{\text{op}}\leq L$ turns out to be a necessary and sufficient condition for the function being L-Lipschitz.

We also get something else for free: The differential operator is a function-valued function, and is allowed to have its own notion of continuity and differentiability. We just needed to attach a notion of norms for its output space. We can now intuitively understand that a function $f$ can be reasonably called continuously differentiable or twice-differentiable via $Df$ being continuous or differentiable.

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
