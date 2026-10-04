# Just Enough Calculus

## 1. Differentiation
Given a function, a useful question often is: what happens to the output when we poke the input slightly. Formally, we ask by how much does the output fluctuate for additive perturbations $x\mapsto x+h$.

If a function is "nice" (doesn't fluctuate drastically; we have some bound on it under small-enough perturbations), in certain cases it makes things easy.

### 1.1 Scalar Functions
As you might recall, for scalar-valued functions on scalar domains $f:\mathbb{R}\to\mathbb{R}$, this is typically defined by a ratio (possible with scalars) and passing the limit of the perturbation to 0. When this limit exists, we define it as the derivative of $f$ at $a$

$$
f'(a):=\lim\limits_{h\to 0}\frac{f(a+h)-f(a)}{h}\equiv \left.\frac{\mathop{df}}{\mathop{dx}} \right\rvert_{x = a}
$$

The changed output under any perturbations $h$ can be approximated by scaling it up by $f'(a)$, and then adding that to the unperturbed function value $f(a)$. That is, we claim, without re-evaluating the function at $a+h$, that:

$$
f(a+h)\approx f(a)+f'(a)h
$$

This approximation is "decent" when $h$ is small. To see why, let's rearrange the definition. Let's subtract $f'(a)$ from both sides and pull it in inside the ratio. The expression pops up at the numerator:

$$
\lim\limits_{h\to 0}\frac{f(a+h)-f(a)-f'(a)h}{h}=0
$$

The numerator, if we think about it, is essentially the error in our approximation (say, $\epsilon$). So, what we have is identical to

$$
\lim\limits_{h\to 0} \frac{\epsilon}{h}=0.
$$

We can stop here. But let's take it one step further. We want to extend derivatives to functions involving arbitrary vectors. Our first hurdle is that we can't be computing ratios anymore. But length (or equivalently, for scalars, absolute-value) is promising. Unfortunately, it doesn't work if we use it directly in the definition. The quantity flips sign depending on whether $h\to 0^+$ or $h\to 0^-`$

$$
\lim\limits_{h\to 0}\frac{f(a+h)-f(a)}{\lvert h\rvert}=\begin{cases}\lim\limits_{h\to 0^+}\frac{f(a+h)-f(a)}{h} & \text{when }h\geq 0; \\ \lim\limits_{h\to 0^-}-\frac{f(a+h)-f(a)}{h} & \text{when }h < 0\end{cases}
$$

However, it works on the reformulated ratio, now that the limit evaluates to $0$ ($0^+\equiv 0^-\equiv 0$)

$$
\lim\limits_{h\to 0} \frac{\epsilon}{h}=\lim\limits_{h\to 0} \frac{\epsilon}{\lvert h\rvert}=0
$$

### 1.2 General Normed Vector-Spaces
Let's consider functions of the form $f:\mathcal{U}\to \mathcal{V}$, where $\mathcal{U}$ and $\mathcal{V}$ are arbitrary vector spaces with just one additional structure: norm (see Just Enough Linear Algebra). The change in the output under a perturbation $\mathbf{h}\in \mathcal{U}$ is the vector $\Delta\mathbf{f}\in\mathcal{V}:=f(\mathbf{a}+\mathbf{h})-f(\mathbf{a})$. It depends on the $\mathbf{h}$ as well $\mathbf{a}$.

#### 1.2.1 Fréchet Differentiability
The influence of $\mathbf{h}$ on the output can be analysed by breaking $\Delta\mathbf{f}$ down into 2 parts - a part that scales linearly with $\mathbf{h}$, and another part that captures all the leftover non-linear influences. This breakdown is valid for any $\mathbf{h}$.

$$
\Delta\mathbf{f}=\underbrace{L_\mathbf{a}(\mathbf{h})}_ {\text{linear}}+\underbrace{E_\mathbf{a}(\mathbf{h})}_{\text{non-linear}}
$$

The motivation is: if the non-linear part is negligible, we can ignore it and use the linear part as our desired approximation of $\Delta\mathbf{f}$. This is reasonable as long as the linear part itself stays bounded. Under this framing, $E_\mathbf{a}(\mathbf{h})$ represents the "error" in our approximation.

To bound this error, similar to the error-ratio we discussed in the scalar case, we consider the ratio of the norms.

To define this cleanly, let's use $\Vert\cdot\Vert_\mathcal{U}$ for the norm on the input space $\mathcal{U}$, and similarly $\Vert\cdot\Vert_\mathcal{V}$ for $\mathcal{V}$. 

As we reduce the magnitude of the perturbation, if the magnitude of the error-term reduces faster, then their ratio vanishes in the limit:

$$
\lim\limits_{\mathbf{h}\to\mathbf{0}} \frac{\Vert E_\mathbf{a}(\mathbf{h}) \Vert_\mathcal{V}}{\Vert \mathbf{h}\Vert_\mathcal{U}}= 0,
$$

That is, we can consider the error to be negligible for small-enough $\mathbf{h}$. We use the small-o notation ($\Vert E_\mathbf{a}(\mathbf{h})\Vert_\mathcal{V}=o(\Vert\mathbf{h}\Vert_\mathcal{U})$ to capture this, and we declare the function to be "differentiable".

Note that we didn't rely on a specific constraint on $L_\mathbf{a}$ for our decomposition to be valid: for any $L_\mathbf{a}$ we pick, one can find a corresponding $E_\mathbf{a}$. Clearly, the ratio doesn't vanish in the limit for any arbitrary choice of $L_\mathbf{a}$. It turns out that there is a unique $L_\mathbf{a}$ that achieves that. See Appendix 1 for a convincing argument.

Since it's unique, it helps to denote it with a special symbol $L^\ast_\mathbf{a}$. We call it the derivative of $f$ at $\mathbf{a}$.

Note that the derivative is a function (or transform, as typically referred to if it's linear) itself with the same domain and co-domain as $f$, i.e., $L^\ast_\mathbf{a}:\mathcal{U}\to V$. It is linear by definition, and it transforms $\mathbf{h}\mapsto L^\ast_\mathbf{x}(\mathbf{h})$ assuring that the following equality holds for every $\mathbf{h}$:

$$
f(\mathbf{a}+\mathbf{h})=f(\mathbf{a})+L^\ast_\mathbf{a}(\mathbf{h})+o(\Vert\mathbf{h}\Vert_\mathcal{U})
$$

#### 1.2.2 Differential Operator
Since the derivative depends on $\mathbf{a}$, we need a way to define it for every $\mathbf{x}\in\mathcal{U}$. This is done by introducing an operator $Df:\mathbf{x}\mapsto L^\ast_\mathbf{x}$. It is called the differential operator (or the "derivative-transform") and has the shape $Df:\mathcal{U}\to(\mathcal{U}\to\mathcal{V})$.

Using the operator notation, the approximation for small $\mathbf{h}$ looks as follows:

$$
f(\mathbf{x}+\mathbf{h})\approx f(\mathbf{x})+ \left((Df)(\mathbf{x})\right)(\mathbf{h})
$$

I've used the functional notation over the traditional $Df(\mathbf{x})[\mathbf{h}]$ to make the operations explicit. Typically it suffices to write $(Df)(\mathbf{x})$ as $Df(\mathbf{x})$.

### 1.4 Special Cases
When we learn about Jacobians and Gradients, they are typically presented in the context of Euclidean spaces (i.e., $\mathbb{R}^d$) and are described in terms of their components. In the following, let's revisit them from Fréchet differentiability perspective. In my opinion, this should help us appreciate the connection as we extend these ideas to more complex cases.

#### 1.4.1 Euclidean Vector-Spaces: Jacobian
For functions such as $f:\mathbb{R}^n\to\mathbb{R}^m$, we can use a trick for the derivative. In finite dimensions, the effect of applying any linear-transform on a vector can be achieved by first finding a matrix of that transform, and then multiplying the vector with that matrix. It is guaranteed that there always is a matrix for every linear-transform (see Just Enough Linear Algebra).

Let's use $f'(\mathbf{x})\in\mathbb{R}^{m\times n}$ for the matrix corresponding to $Df(\mathbf{x})$ for the usual choice of basis (along the co-ordinate axes). Then, for a small-enough $\mathbf{h}$, the linear approximation becomes

$$
f(\mathbf{x}+\mathbf{h})\approx f(\mathbf{x})+ \left(Df(\mathbf{x})\right)(\mathbf{h})=f(\mathbf{x})+f'(\mathbf{x})\mathbf{h}
$$

With this, we get an evaluation rule similar to the scalar-case. We call the matrix the Jacobian, and use the notation $J_{\mathbf{x}}f$.

#### 1.4.2 Scalar-valued Functions on Hilbert Spaces: Gradient Vector
Gradients are much more interesting than they appear at first. In this section, we discuss a slightly different perspective on what they are.

Let's consider scalar-valued functions $f:\mathcal{H}\to\mathbb{R}$ on complete inner-product spaces $\mathcal{H}$ (see Just Enough Linear Algebra). We can use another trick for the derivatives in such cases.

For every bounded linear-transform $L:\mathcal{H}\to\mathbb{R}$, there always is a unique vector $\boldsymbol{\varphi}_L$ inside $\mathcal{H}$ itself that replicates effect of transformation via $L$. It does so with a simple inner product defined on the input space, i.e., that for every $\mathbf{h}\in\mathcal{H}$, we have $L(\mathbf{h})=\langle \boldsymbol{\varphi}_L, \mathbf{h}\rangle _{\mathcal{H}}$. This result holds as the space defined by the linear transforms (dual space) is the same as the original vector space (Riesz Representation Theorem), which isn't always the case (See Just Enough Linear Algebra).

For the derivative of $f$ at $\mathbf{x}$, which is nothing but a linear transform, we reserve a special notation $\nabla_\mathbf{x} f$ (instead of $\varphi$), so that we can write

$$
(Df(\mathbf{x}))(\mathbf{h})=\langle \nabla_\mathbf{x} f, \mathbf{h}\rangle _{\mathcal{H}}
$$

Now, back to functions on Euclidean domains $f:\mathbb{R}^n\to\mathbb{R}$, this happens to be equal to the transpose of the Jacobian component-by-component to make the algebra work (as $J_\mathbf{x}f$ is the row matrix $\mathbb{R}^{1\times n}$):

$$
\nabla_\mathbf{x} f=J_\mathbf{x}f^\top
$$

Replacing the inner-product by its finite-dimensional counterpart, the dot-product, we rewrite our approximation rule:

$$
f(\mathbf{x}+\mathbf{h})\approx f(\mathbf{x})+f'(\mathbf{x})\mathbf{h}=f(\mathbf{x})+\nabla_\mathbf{x} f\cdot\mathbf{h}
$$

### 1.5 More Special Cases
The sophisticated machinery for differentiability a la Fréchet pays off as it allows us to extend derivatives to functions on any normed space. We look at couple of interesting ones in this section.

#### 1.5.1 Derivatives of Matrix-Functions: Jacobian Tensor & Gradient Matrix
Recall that the space of matrices is a vector space on its own right, and the fact that matrix norms exist. For functions defined on matrices $f:\mathbb{R}^{m\times n}\to\mathbb{R}^k$, all of the discussion around derivatives work. The only change is in the dimensions involved:

- The Jacobian $J_\mathbf{x}f$ is the tensor of shape $\mathbb{R}^{k\times m\times n}$ (output dimension always is the first dimension).
- For $f:\mathbb{R}^{m\times n}\to\mathbb{R}$, we also have the gradient but as the matrix $\nabla_\mathbf{x} f\in \mathbb{R}^{m\times n}$ (since the first dimension of the Jacobian is $1$)

#### 1.5.2 Gradient of a Functional involving Probability Densities
In this section, we consider an example that is particularly relevant for the transport problem.

TODO

### 1.6 Functions with Bounded Derivative: Lipschitz Functions
Let's revisit the original promise of derivatives as discussed in the first section - helping us finding "nice" functions. We keep the context on general normed spaces. 

#### Continuous differentiability
Compact + continuous map -> bounded

#### Lipscthitz
One of the ways we recognise well-behaved functions is by passing multiple inputs through it and putting bounds on how far apart they are allowed to land from one another. Lipschitz continuity captures this formally with distances via the norm.

We call a function L-Lipschitz as long as we can find an $L\geq 0$ such that every input pair $\mathbf{x},\mathbf{y}$ bounds the distance between their images by their own distance, up to a multiplicative factor of $L$, i.e.,

$$
\Vert f(\mathbf{x})-f(\mathbf{y})\Vert_\mathcal{V}\leq L\Vert\mathbf{x}-\mathbf{y}\Vert_\mathcal{U}
$$

This should be connected to differentiability in some way as the pair can be arbitrary close to one another. We formalise this by defining a norm of the differential operator and putting $L$ as an upper bound on it. Intuitively, this norm (like every operator norm) should capture the "blow-up" factor on its input.

To define the operator norm, we first use the fact that derivative at any $\mathbf{x}$ is just a linear-transform and its own norm represents the maximum stretch-factor for any $\mathbf{h}$:

$$
\Vert Df(\mathbf{x})\Vert_\infty:=\sup\limits_{\mathbf{h}\in \mathcal{U}; \mathbf{h}\neq \mathbf{0}}\frac{\Vert (Df(\mathbf{x}))(\mathbf{h})\Vert_\mathcal{V}}{\Vert\mathbf{h}\Vert_\mathcal{U}}
$$

For Euclidean space, this is simply the largest singular value of the Jacobian matrix.

The operator norm then captures the maximum of those across the entire domain:

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
