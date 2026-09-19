# A working MLE's guide to SOTA generative models
Published in September 2026

I recently gave a talk at work on state-of-the-art (SOTA) generative models, and I've been thinking of polishing my personal notes ever since. [These](https://uselesstechjunks.github.io/generative_models_mle/index.html) are the result, designed to be entirely self-sufficient, even without access to the original slides.

## Scope and Focus
Here, I keep the focus entirely on non-autoregressive generation. While autoregressive generation standards (token-by-token generation) are steadily improving, flow- and diffusion-based models remain the standard across modalities - from images and video to protein structure synthesis - to this day. At the same time, the novelty of the underlying mathematical framework makes these models a fascinating subject to study.

I deliberately omit neural architecture breakdowns for two reasons:
- It wasn't architectural tweaks that drove recent SOTA performance; it was the mathematical breakthrough of stochastic interpolants that unified flow and diffusion under a single framework, making training remarkably easier.
- The core architectural components should already be familiar to MLEs with a working knowledge of transformers. (Variational autoencoders are the one exception, but they deserve their own dedicated deep dive).

Today, the most capable models - whether for images (Nano Banana Pro), videos (MiniMax H3), or protein synthesis (AlphaFold 3) - rely on this flow and diffusion framing established by stochastic interpolants. Cultivating an intuitive grasp of that framework is the core focus of this article.

## For people who are familiar with DDPM
If you are accustomed to original diffusion models like DDPM, expect a paradigm shift: the traditional forward and reverse processes are absent here. This modern framework is significantly more pedagogically sound. Chapter 3 provides a brief retrospective on those earlier models to bridge the gap.
