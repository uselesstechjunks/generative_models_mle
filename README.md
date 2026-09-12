# A working MLE's guide to SOTA generative models
Published in September 2026

I recently gave a talk at work on SOTA generative models, and [these](https://uselesstechjunks.github.io/generative_models_mle/index.html) are my companion notes for that presentation. While I am unable to share the content of the slides here, the material covered in this article is designed to be self-sufficient.
    
## A few words about the scope
I have limited the scope to understanding models that generate samples for various modalities in a non-autoregressive way. While autoregressive models are steadily improving, flow- and diffusion-based models are still (at the time of writing) considered state-of-the-art (SOTA) across modalities such as images, videos, and protein structure synthesis.

I deliberately do not cover the neural architectures of these models. This choice was made primarily for two reasons: (a) it wasn't architectural innovations that made these models SOTA, but rather the mathematical insight that unified flow and diffusion models under a single framework, making training impressively easier; and (b) the architectural components of these models should already be familiar to MLEs with a working knowledge of transformer architecture. The one exception is variational autoencoders (VAEs), which I believe deserve a separate article in their own right.

Currently, most SOTA models across modalities (images: Nano Banana Pro, videos: MiniMax H3, protein synthesis: AlphaFold 3) use the flow/diffusion framing established by the stochastic interpolants formulation. Gathering an intuitive understanding of how these models work is the primary focus of this article.

## A few words for people who know DDPM
Readers familiar with the original diffusion models (e.g., DDPM) might find a few concepts presented differently (e.g., there are no forward or reverse processes). However, the new framework is more pedagogically sound. A brief callout to earlier diffusion models is made in Chapter 3.
