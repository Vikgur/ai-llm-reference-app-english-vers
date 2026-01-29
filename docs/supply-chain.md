# Table of Contents

- [Supply Chain Security](#supply-chain-security)
- [Supply Chain Objects](#supply-chain-objects)
- [Code as Artifact](#code-as-artifact)
- [Model as Artifact](#model-as-artifact)
- [Configuration as Artifact](#configuration-as-artifact)
- [SBOM](#sbom)
- [Attestations and Provenance](#attestations-and-provenance)
- [Signatures and Trust Policy](#signatures-and-trust-policy)
- [Policy Enforcement](#policy-enforcement)
- [Relation to CI/CD Platform](#relation-to-cicd-platform)
- [Relation to SECURITY.md](#relation-to-securitymd)
- [Conclusion](#conclusion)

---

# Supply Chain Security

This document describes the **supply chain model** for `ai-llm-reference-app`.

Goal:  
– demonstrate a mature DevSecOps approach  
– establish a trusted delivery model  
– connect code, model, and configuration into a single chain of trust  

The repository **consumes** the supply chain, not fully implements it.

Source of truth:  
**ai-secure-ci-cd-platform**

---

# Supply Chain Objects

The supply chain involves three classes of artifacts:

– application code  
– model (weights + metadata)  
– configuration and manifests  

All three are treated as:  
– versioned  
– immutable artifacts  
– integrity-verified objects  

---

# Code as Artifact

Code:  
– is built into a container image  
– undergoes static analysis  
– is fixed by digest  

For code, the following are generated:  
– SBOM  
– provenance  
– signature  

Source code without a verified build is **not considered trusted**.

---

# Model as Artifact

The model is treated as:  
– a binary object  
– with a separate lifecycle  
– of high value  

For the model, the following are ensured:  
– checksum (SHA-256)  
– version  
– model card  
– immutability  

The model:  
– is not downloaded at runtime  
– is not modified  
– is not dynamically generated  

---

# Configuration as Artifact

Configuration includes:  
– runtime parameters  
– security policies  
– deployment manifests  

It:  
– is versioned  
– undergoes policy validation  
– is part of provenance

---

# SBOM

SBOMs are generated for the project:

– for the application image  
– for dependencies  
– for the model (metadata-level)  

SBOMs are used for:  
– auditing  
– compliance  
– vulnerability analysis  

SBOMs are stored in:  
`security/sbom/`

---

# Attestations and Provenance

Each artifact is accompanied by:

– build provenance  
– verification results  
– policy evaluation  

Attestations:  
– are signed  
– are verified at deployment  
– are mandatory  

Storage:  
`security/attestations/`

---

# Signatures and Trust Policy

Artifacts:  
– are signed in CI  
– are verified before use  

Trust policy defines:  
– who can build  
– what is considered valid  
– which checks are mandatory  

Without policy compliance, an artifact **is not allowed to run**.

---

# Policy Enforcement

Policy enforcement is applied:

– during CI  
– when publishing artifacts  
– at deployment in Kubernetes  

Policies are formalized and machine-readable.

---

# Relation to CI/CD Platform

The supply chain implementation resides in:  
**ai-secure-ci-cd-platform**

This repository:  
– consumes prebuilt artifacts  
– does not duplicate pipeline logic  
– demonstrates integration  

---

# Relation to SECURITY.md

The supply chain is part of the security scope:  
– protection against tampering  
– protection against replacement  
– proof of provenance  

See:  
[`SECURITY.md`](../SECURITY.md)

---

# Conclusion

The supply chain in `ai-llm-reference-app` is:  
– formalized  
– verifiable  
– reproducible  

It is designed for environments where:  
**trust must be cryptographically proven**.
