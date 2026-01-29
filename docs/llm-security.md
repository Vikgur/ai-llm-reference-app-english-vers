# Table of Contents

- [LLM Security](#llm-security)
- [Security Context](#security-context)
- [LLM Threat Model](#llm-threat-model)
- [Mapping Threats to the LLM Pipeline](#mapping-threats-to-the-llm-pipeline)
- [Prompt Injection](#prompt-injection)
  - [Description](#description)
  - [Countermeasures](#countermeasures)
- [Data Exfiltration](#data-exfiltration)
  - [Description](#description-1)
  - [Countermeasures](#countermeasures-1)
- [Policy Bypass](#policy-bypass)
  - [Description](#description-2)
  - [Countermeasures](#countermeasures-2)
- [Denial of Service](#denial-of-service)
  - [Description](#description-3)
  - [Countermeasures](#countermeasures-3)
- [Model Tampering](#model-tampering)
  - [Description](#description-4)
  - [Countermeasures](#countermeasures-4)
- [Input Controls](#input-controls)
- [Inference Controls](#inference-controls)
- [Output Controls](#output-controls)
- [Runtime Isolation Assumptions](#runtime-isolation-assumptions)
- [Relation to Formal Threat Model](#relation-to-formal-threat-model)
- [Conclusion](#conclusion)

---

# LLM Security

This document describes the **LLM security model** implemented in `ai-llm-reference-app`.

Goal:  
– to capture threats specific to LLMs  
– to show where and how they are controlled  
– to connect the model, code, and policies  

The document focuses on **inference**, not training.

---

# Security Context

In a sovereign environment, LLMs are considered:  
– a potential source of data leaks  
– a component difficult to interpret  
– an object of high interest for attackers  

Security is built on the assumption:  
**the model itself is not trusted**.

Architectural context:  
[`architecture.md`](architecture.md)

---

# LLM Threat Model

Key threat classes:

– Prompt Injection  
– Data Exfiltration  
– Policy Bypass  
– Denial of Service  
– Model Tampering  

Each threat is considered **in relation to inference stages**.

---

# Mapping Threats to the LLM Pipeline

| Stage | Potential Threats |
|-------|------------------|
| Prompt / Input | Injection, DoS |
| Tokenization | Boundary bypass |
| Embeddings | Side-channel |
| Transformer | Resource exhaustion |
| Sampling | Non-deterministic leakage |
| Decoding | Policy bypass |
| Post-processing | Output leakage |

Pipeline is detailed in:  
[`llm-internals.md`](llm-internals.md)

---

# Prompt Injection

## Description

Attempts to:  
– alter the model’s behavior  
– bypass restrictions  
– make the model produce forbidden content  

## Countermeasures

– strict input validation  
– length limits  
– deny-by-default policies  
– no system prompts  

---

# Data Exfiltration

## Description

Risks:  
– data leaks through output  
– model information reconstruction  
– side-channel via generation  

## Countermeasures

– output filtering  
– redaction  
– response length limits  
– no access to external data

---

# Policy Bypass

## Description

Attempts to:  
– bypass security filters  
– alter enforcement logic  
– use non-standard tokens  

## Countermeasures

– centralized policies  
– formalized rules  
– multi-stage validation  

Policies are implemented in:  
`ci/policies/*.rego`

---

# Denial of Service

## Description

Possible attacks:  
– long prompts  
– resource-intensive sequences  
– repeated requests  

## Countermeasures

– length limits  
– resource caps  
– timeouts  
– Kubernetes quotas

---

# Model Tampering

## Description

Attempts to:  
– modify weights  
– replace artifacts  
– load an unsigned model  

## Countermeasures

– immutable model  
– checksum verification  
– read-only filesystem  
– supply chain validation  

CI/CD relation:  
[`supply-chain.md`](supply-chain.md)

---

# Input Controls

Input control includes:

– format validation  
– length restrictions  
– allowed characters  
– deny-by-default  

Input is treated as **completely untrusted**.

---

# Inference Controls

Inference process control:

– deterministic operations  
– limited sampling  
– fixed sizes  
– predictable resource usage  

Inference should be:  
**explainable and reproducible**.

---

# Output Controls

Output undergoes:

– filtering  
– redaction  
– policy evaluation  
– final validation  

Output is the last line of defense.

---

# Runtime Isolation Assumptions

Security assumes:

– isolated Kubernetes namespace  
– non-privileged pod  
– seccomp / AppArmor  
– no external calls  
– read-only filesystem  

Runtime is described in:  
[`architecture.md`](architecture.md)

---

# Relation to Formal Threat Model

This document complements, but does not replace:

– `security/threat-model/threat-model.md`  

It describes **applied threat implementation**, not a formal methodology.

---

# Conclusion

LLM security in this project is:  
– threat-driven  
– policy-enforced  
– pipeline-aware  

It is designed for environments where:  
**the LLM must be controlled, not “smart”**.
