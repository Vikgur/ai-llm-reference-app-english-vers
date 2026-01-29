# Table of Contents

- [System Architecture](#system-architecture)
- [Architectural Context](#architectural-context)
- [Logical Architecture](#logical-architecture)
- [System Components](#system-components)
  - [API Layer](#api-layer)
  - [LLM Inference Pipeline](#llm-inference-pipeline)
  - [Policy Enforcement](#policy-enforcement)
  - [Model Artifacts](#model-artifacts)
  - [Observability](#observability)
- [Data Flow](#data-flow)
- [Trust Boundaries](#trust-boundaries)
  - [Untrusted Zone](#untrusted-zone)
  - [Partially Trusted Zone](#partially-trusted-zone)
  - [Trusted Zone](#trusted-zone)
- [Runtime Architecture](#runtime-architecture)
- [Kubernetes Topology](#kubernetes-topology)
- [Security Enforcement Points](#security-enforcement-points)
- [Related Documents](#related-documents)
- [Summary](#summary)

---

# System Architecture

This document describes the **logical and runtime architecture** of `ai-llm-reference-app`.

Purpose:  
– define system components  
– outline the inference data flow  
– identify trust boundaries  
– indicate where and how security enforcement is applied  

The document describes **what and where**, not implementation details.

---

# Architectural Context

`ai-llm-reference-app` is an **inference application** operating as part of the Sovereign AI platform.

The system:  
– does not train the model  
– does not manage infrastructure  
– does not handle governance  

It:  
– receives requests  
– performs controlled inference  
– returns verified results

---

# Logical Architecture

The system is divided into explicit logical components:

– API layer  
– LLM inference pipeline  
– Policy enforcement  
– Model artifacts  
– Observability  

Each component has:  
– a clear responsibility  
– limited dependencies  
– defined trust boundaries  

---

# System Components

## API Layer

Purpose:  
– receive requests  
– perform basic validation  
– enforce format control  

The API **does not contain model logic** and has no direct access to model weights.

---

## LLM Inference Pipeline

Inference is implemented as a **sequential pipeline**:

1. Tokenization  
2. Embeddings  
3. Transformer decoder  
4. Logits and sampling  
5. Decoding  
6. Post-processing  

Each stage is:  
– deterministic  
– logically isolated  
– subject to control  

Stage details:  
[`llm-internals.md`](llm-internals.md)

---

## Policy Enforcement

Security policies are applied:  
– at input  
– between inference stages  
– at output  

Policies are:  
– formalized  
– verifiable  
– independent of UX  

Threat model reference:  
[`llm-security.md`](llm-security.md)

---

## Model Artifacts

The model is treated as:  
– an immutable artifact  
– a versioned object  
– an integrity-controlled entity  

Weights are prohibited from:  
– runtime modification  
– dynamic loading  
– side effects  

---

## Observability

The system publishes:  
– inference metrics  
– security events  
– policy violation signals  

Observability is used:  
– for control  
– for auditing  
– to prove correctness

---

# Data Flow

The complete data flow is as follows:

Client  
↓  
API  
↓  
Tokenization  
↓  
Embeddings  
↓  
Transformer  
↓  
Sampling / Decoding  
↓  
Post-processing  
↓  
Response

Data **does not cross component boundaries arbitrarily**.  
Each transition is a controlled point.

---

# Trust Boundaries

The system separates trust zones:

## Untrusted Zone

– external user  
– input prompt  
– network environment  

## Partially Trusted Zone

– API layer  
– preprocessing  

## Trusted Zone

– inference engine  
– model artifacts  
– runtime policies  

Transitions between zones are always:  
– validated  
– logged  
– controlled

---

# Runtime Architecture

At runtime, the system is deployed as:

– a containerized application  
– an isolated pod  
– read-only filesystem  
– constrained resources  

External interaction:  
– only via API  
– no direct storage access  
– no external calls  

---

# Kubernetes Topology

In Kubernetes, the following are used:

– dedicated namespace  
– resource quotas  
– Pod Security Standards  
– seccomp / AppArmor  
– NetworkPolicies  

The application has no:  
– cluster-wide permissions  
– privileged containers  
– dynamic volume mounts

---

# Security Enforcement Points

Security enforcement occurs:

– at the API level  
– inside the inference pipeline  
– at the artifact level  
– at the runtime level  
– at the CI/CD level  

The architecture assumes that **security cannot be “added later”**.

---

# Related Documents

– LLM pipeline details: [`llm-internals.md`](llm-internals.md)  
– Threat model and security: [`llm-security.md`](llm-security.md)  
– Supply chain and artifacts: [`supply-chain.md`](supply-chain.md)  

---

# Summary

The architecture of `ai-llm-reference-app` is:  
– minimal  
– formal  
– controllable  

It is intended for environments where:  
**every byte and every transition must be explainable and verifiable**.
