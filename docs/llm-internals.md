# Table of Contents

- [LLM Internals](#llm-internals)
- [Model Architectural Choices](#model-architectural-choices)
- [Overall Inference Pipeline](#overall-inference-pipeline)
- [Tokenization](#tokenization)
  - [What is Used](#what-is-used)
  - [Why This Way](#why-this-way)
  - [Constraints](#constraints)
- [Embeddings](#embeddings)
  - [Token Embeddings](#token-embeddings)
  - [Positional Embeddings](#positional-embeddings)
- [Self-Attention](#self-attention)
- [Feed-Forward Network (FFN)](#feed-forward-network-ffn)
- [Logits and Sampling](#logits-and-sampling)
- [Decoding](#decoding)
- [Post-processing](#post-processing)
- [Model Constraints](#model-constraints)
- [Attack Surfaces](#attack-surfaces)
- [Code Navigation](#code-navigation)
- [Summary](#summary)

---

# LLM Internals

This document describes the **internal structure of the LLM** implemented in `ai-llm-reference-app`.

Purpose:  
– demonstrate conscious understanding of LLM architecture  
– capture adopted simplifications  
– define model applicability boundaries  
– provide a basis for threat modeling  

This is a **reference implementation**, not a production-grade model.

---

# Model Architectural Choices

A **decoder-only Transformer** is used.

Reasons for this choice:  
– aligns with modern autoregressive LLMs  
– minimal component count  
– transparent for analysis  
– convenient for controlling inference  

The model:  
– does not support encoder-decoder schemes  
– does not use MoE  
– contains no external memory

---

# Overall Inference Pipeline

Inference consists of sequential stages:

1. Tokenization  
2. Token + positional embeddings  
3. Self-attention  
4. Feed-forward network  
5. Logits computation  
6. Sampling  
7. Decoding and post-processing  

Each stage:  
– is implemented explicitly  
– is logically separated  
– serves as an individual control point  

Architectural context:  
[`architecture.md`](architecture.md)

---

# Tokenization

## What is Used

A **deterministic vocabulary-based tokenization** is used.

Characteristics:  
– fixed vocabulary  
– no dynamic training  
– reproducible

## Why This Way

– minimal attack surface  
– predictable behavior  
– simplified input analysis  

## Constraints

– limited vocabulary  
– no subword optimizations  
– not suitable for full real-world language coverage  

---

# Embeddings

## Token Embeddings

Each token is mapped to:  
– a fixed-dimension vector  
– without contextual dynamics  

## Positional Embeddings

Positional embeddings are used:  
– to preserve token order  
– without relative positions  

The choice favors:  
– simplicity  
– readability  
– predictability

---

# Self-Attention

Self-attention is conceptually implemented as:

– computation of Q, K, V  
– scaled dot-product  
– softmax normalization  
– weighted summation  

Purpose of the implementation:  
– demonstrate the mechanism, not optimization  
– maintain transparency  
– simplify analysis of token dependencies  

The model is **not optimized for memory or speed**.

---

# Feed-Forward Network (FFN)

The FFN implements:  
– position-independent transformation  
– non-linearity  
– expansion and compression of dimensions  

FFN:  
– identical across all positions  
– contains no conditional logic 

---

# Logits and Sampling

After the decoder block, the following are computed:  
– logits for each vocabulary token  

Sampling:  
– simplified  
– no complex strategies  
– deterministic-oriented  

Purpose:  
– output controllability  
– minimize unexpected behavior  

---

# Decoding

Decoding performs:  
– conversion of tokens to text  
– length control  
– forbidden sequence filtering  

Decoding is a **critical security point** because:  
– output is generated here  
– potential data leakage can occur  

Related to threat model:  
[`llm-security.md`](llm-security.md)

---

# Post-processing

Post-processing is applied for:  
– output filtering  
– redaction  
– policy enforcement  

It serves as the final barrier between the model and the user.

---

# Model Constraints

Key constraints to understand:

– model is not trained on real-world corpora  
– generation quality is not the goal  
– model does not scale horizontally  
– no batching support  
– no streaming inference  

These constraints are **intentional**.

---

# Attack Surfaces

Main attack surfaces:  
– input prompt  
– tokenization  
– sampling and decoding  
– post-processing  

Each is addressed in:  
[`llm-security.md`](llm-security.md)

---

# Code Navigation

The implementation is located in:

– `app/llm/tokenizer/`  
– `app/llm/embeddings/`  
– `app/llm/transformer/`  
– `app/llm/decoding/`  
– `app/llm/postprocess/`  

This document does not duplicate the code but **provides a mental model**.

---

# Summary

This LLM implementation is:  
– minimal  
– deterministic  
– transparent  

It is designed so that:  
**it can be analyzed, secured, and formally described**.
