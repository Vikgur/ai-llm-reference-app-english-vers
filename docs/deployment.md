# Table of Contents

- [Deployment Model](#deployment-model)
- [Deployment Context](#deployment-context)
- [Container Assumptions](#container-assumptions)
- [Kubernetes Deployment Model](#kubernetes-deployment-model)
- [Namespace Isolation](#namespace-isolation)
- [Resource Isolation](#resource-isolation)
- [Security Controls in Kubernetes](#security-controls-in-kubernetes)
- [Network Model](#network-model)
- [Secrets and Configuration](#secrets-and-configuration)
- [Observability Hooks](#observability-hooks)
- [Runtime Controls](#runtime-controls)
- [Constraints for Prod-like Environments](#constraints-for-prod-like-environments)
- [Helm and K8s Manifest Integration](#helm-and-k8s-manifest-integration)
- [Summary](#summary)

---

# Deployment Model

This document describes the **secure path from artifact to runtime** for `ai-llm-reference-app`.

Purpose:  
– capture environment assumptions  
– describe the deployment model  
– show where runtime security is applied  
– outline constraints for prod-like environments  

The document answers:  
**how this LLM should be safely deployed**.

---

# Deployment Context

The application is deployed as part of the Sovereign AI platform.

It:  
– does not manage the cluster  
– does not modify infrastructure  
– does not require privileges  

Architectural context:  
[`architecture.md`](architecture.md)

---

# Container Assumptions

The container is treated as:

– immutable  
– minimal  
– non-privileged  

Key assumptions:  
– single process  
– no shell access  
– read-only filesystem  
– no package manager  

The container is not intended for interactive use.

---

# Kubernetes Deployment Model

The application is deployed as:

– Deployment  
– one or more replicas  
– stateless workload  

Each pod:  
– is isolated  
– does not persist state  
– does not share volumes with other pods

---

# Namespace Isolation

The application uses:

– a dedicated namespace  
– its own quotas  
– limited permissions  

The namespace:  
– does not have cluster-admin rights  
– does not interact directly with other workloads  

---

# Resource Isolation

Resource constraints are mandatory:

– CPU limits  
– memory limits  
– pod count limits  

Purpose:  
– DoS protection  
– predictable inference  
– consumption control

---

# Security Controls in Kubernetes

The following measures are applied:

– Pod Security Standards  
– seccomp profiles  
– AppArmor profiles  
– NetworkPolicies  

The application:  
– does not use privileged mode  
– has no hostPath mounts  
– does not use hostNetwork  

---

# Network Model

Network assumptions:

– ingress only via Service  
– egress traffic is restricted  
– no external API calls  

NetworkPolicies are used as:  
– an enforcement mechanism  
– part of the threat model

---

# Secrets and Configuration

Secrets:  
– delivered via Kubernetes Secrets  
– not stored in the image  
– not logged  

Configuration:  
– mounted read-only  
– versioned  
– validated  

---

# Observability Hooks

The application exposes:

– metrics endpoint  
– structured logs  
– trace hooks  

Observability is used for:  
– behavior control  
– auditing  
– anomaly detection  

Configuration path:  
`observability/`

---

# Runtime Controls

Runtime controls include:

– syscall restrictions  
– disk write prohibition  
– network access control  
– resource limitations  

Related to security model:  
[`llm-security.md`](llm-security.md)

---

# Constraints for Prod-like Environments

Environments must provide:

– secure registry  
– signature verification  
– trust policy enforcement  
– audit logging  

Without these, deployment is considered **non-compliant**.

---

# Helm and K8s Manifest Integration

Deployment implementation:  
– `helm/`  
– `k8s/`  

This document:  
– does not duplicate YAML  
– captures architectural requirements  

---

# Summary

The deployment model of `ai-llm-reference-app` is:  
– minimal  
– isolated  
– controllable  

It is intended for environments where:  
**runtime is an extension of the security model, not a separate layer**.
