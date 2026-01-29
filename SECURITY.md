## Table of Contents

- [Security Policy](#security-policy)
- [Security Scope](#security-scope)
- [Out of Scope / Non-Goals](#out-of-scope--non-goals)
- [Supported Versions](#supported-versions)
- [What Constitutes a Security Issue](#what-constitutes-a-security-issue)
- [Vulnerability Disclosure Process](#vulnerability-disclosure-process)
- [Response Expectations](#response-expectations)
- [Threat Model and Security Architecture](#threat-model-and-security-architecture)
- [Supply Chain Security](#supply-chain-security)
- [Reporting Vulnerabilities](#reporting-vulnerabilities)
- [Final Provisions](#final-provisions)

---

# Security Policy

This document defines the **security governance** of the `ai-llm-reference-app` project.

The project is intended for use in **regulated, sovereign, and high-assurance environments**.  
Security is treated as an architectural characteristic, not an after-the-fact check.

---

# Security Scope

The project's security scope includes:

– LLM inference pipeline  
– API and input/output handling  
– security guards and policy enforcement  
– the model as an immutable artifact  
– CI/CD and supply chain  
– Kubernetes runtime configuration  
– observability and audit signals  

Security covers **code, model, artifacts, runtime, and delivery processes**.

---

# Out of Scope / Non-Goals

Not considered within the security scope:

– generation quality and hallucinations  
– training and fine-tuning  
– third-party hosted LLM services  
– end-user UX  
– performance and latency optimizations  
– non-production environments outside the described architecture  

The project is not a bug bounty program.

---

## Supported Versions

Supported versions include:

– the latest `main` branch  
– all releases with up-to-date documentation and CI/CD attestation  

Artifacts lacking:  
– SBOM  
– checksum  
– provenance  

are considered **unsupported**.

---

## What Constitutes a Security Issue

Security vulnerabilities include:

– bypassing policy enforcement  
– violation of trust boundaries  
– data leakage through LLM output  
– tampering with the model or weights  
– compromise of the supply chain  
– breach of runtime isolation  
– circumvention of audit and observability  

Functional bugs and output quality issues are **not considered** security vulnerabilities.

---

# Vulnerability Disclosure Process

Responsible vulnerability disclosure is encouraged.

Process:
1. Prepare a detailed description of the issue  
2. Specify the affected version, commit, or artifact  
3. Provide a PoC or reproduction scenario  
4. Submit the report privately (see contacts below)  

Public disclosure **prior to coordination** is not recommended.

---

# Response Expectations

Expected response to a valid report:

– acknowledgment of receipt  
– triage and classification  
– analysis of architectural impact  
– fix or documented mitigation  
– documentation updates if required  

Timelines depend on the severity and nature of the vulnerability.

---

# Threat Model and Security Architecture

The threat model and security architecture are described separately:

– Threat model: `security/threat-model/threat-model.md`  
– LLM security: `docs/llm-security.md`  

SECURITY.md does not duplicate the threat model, but **sets rules for its application**.

---

# Supply Chain Security

Supply chain security is part of the security scope:

– model integrity  
– artifact immutability  
– provenance  
– policy-based validation  

Details: [`docs/supply-chain.md`](docs/supply-chain.md)

---

# Reporting Vulnerabilities

For reporting security vulnerabilities, use:  
– private channels listed in the repository's `SECURITY.md`  
– or the owners listed in `CODEOWNERS`  

Do not create public issues for security reports.

---

# Final Provisions

This project:  
– is oriented towards threat-driven security  
– uses a policy-first approach  
– is intended for environments where **trust must be provable**  

Security here is a contract, not a promise.
