# Just Enough Calculus

## Frechet Differentiability
Given a function, a common inquiry regarding it's nature is to ask: what happens to the output of the function when we perturb the input slightly? The idea is: if the function doesn't behave crazy (i.e., we have some bound on how much it fluctuates for small-enough changes), we can establish certain properties of the functions which are useful. For functions in general vector space, Frechet derivative captures this notion. 

Let's assume that we have a function $f:U\to V$, $U$ and $V$ being some vector space where norm is defined (i.e., we can compute length of these vectors). A perturbation $\mathbf{x}\mapsto\mathbf{x}+\boldsymbol{\delta}$ causes a change in the output $f(\mathbf{x})\mapsto f(\mathbf{x}+\boldsymbol{\delta})$. The difference vector, $\boldsymbol{\delta}\mathbf{f}:=f(\mathbf{x}+\boldsymbol{\delta})-f(\mathbf{x})$, clearly dependent on the perturbation $\boldsymbol{\delta}\in U$ as well as the point of evaluation (i.e., $\mathbf{x}\in U$), can be thought of decomposing into 2 parts - a linear (in $\boldsymbol{\delta}$) approximation of the function near the vicinity and non-linear error-term of that approximation:

$$
\boldsymbol{\delta}\mathbf{f}:=f(\mathbf{x}+\boldsymbol{\delta})-f(\mathbf{x})=\underbrace{g_{\mathbf{x}}(\boldsymbol{\delta})}_{\text{linear approx}}+\underbrace{h_{\mathbf{x}}(\boldsymbol{\delta})}_{\text{non-linear error}}
$$

To bound the error, we check the ratio $\frac{\parallel h_{\mathbf{x}}(\boldsymbol{\delta}) \parallel}{\parallel \boldsymbol{\delta}\parallel}$. As we reduce the perturbation, if the magnitude of the error stays bounded by the magnitude of the perturbation itself, i.e.,  

$$
\lim\limits_{\boldsymbol{\delta}\to 0} \frac{\parallel h_{\mathbf{x}}(\boldsymbol{\delta}) \parallel}{\parallel \boldsymbol{\delta}\parallel}= 0,
$$

we consider the error to be negligible. In such cases, we consider the function to be "differentiable", use small-oh notation for the error (i.e., $h_{\mathbf{x}}(\boldsymbol{\delta})=o(\parallel\boldsymbol{\delta}\parallel)$), and call $g_{\mathbf{x}}(\boldsymbol{\delta})$ the derivative of the function at $\mathbf{x}$.

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
