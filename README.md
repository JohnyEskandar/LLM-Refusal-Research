# LLM Refusal Research

Investigating how refusal behavior is represented internally in small language models, using activation steering on Qwen-1.8B-Chat.

## Overview

Most work on LLM refusal treats it as a single linear direction in activation space. We tested whether that holds up across different categories of harmful content, using prompts from SORRY-Bench across four categories: HateSpeech, CrimeAssistance, Inappropriate, and Advice.

## Method

We extracted refusal directions at each layer by contrasting activations on harmful vs. benign prompts, then used ablation to test how removing each direction affected the model's refusal behavior. Layer 14 came out as the strongest refusal layer, with a much sharper score drop than any other layer in the network.

## Key findings

- **Layer 14 is the strongest refusal layer** — score dropped from roughly 1.6 to -6.4 when the direction was ablated, far more than any other layer
- **Cross-category ablation achieved 84-96% bypass rates**, meaning a refusal direction extracted from one harm category often suppressed refusal in others too
- **CrimeAssistance transferred most strongly** across categories, while HateSpeech was the most distinct
- **Cosine similarities between category directions ranged from 0.735 to 0.892** — high, but not high enough to call these the same direction. This points toward refusal living in a conic subspace rather than a single line, which lines up with related findings in Joad et al. (2026)

## Why this matters

If refusal is a subspace rather than a single direction, safety interventions that assume a single steering vector may be incomplete. This has implications for how robust current refusal-based safety training actually is.

## Team

Built with Amith Chintalapati, Viraaj Singh, and Cole Heutten. Original repo [here](https://github.com/amithchintalapati/LLM-Refusal-Research).

## Status

Unpublished, exploratory research. Open to feedback.
