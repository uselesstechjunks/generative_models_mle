# Chapter 0: Preliminaries

These should be familiar to you - the following is meant for a quick refresher.

## Probability
We're dealing with a probability space where we have sample space $\Omega$

We only need a handful of theorems here.

### Joint and marginal densities

### Bayes' theorem

### Expectations

## Calculus
TODO

Some placeholder math below:
- Dataset: $D=(z_i)_{i=1}^N, z_i\in\mathbb{R}^d$.
- The Goal: Learn a map $T$ that morphs some distribution $p$ to target $q$.

  $$
  T_\sharp p=q
  $$

- Optimal Transport: For some cost function $c:\mathbb{R}^d\times\mathbb{R}^d\to\mathbb{R}_{\geq 0}$

  $$
  \inf_T\mathbb{E}_{x\sim\mu}[c(x, T(x)]
  $$
