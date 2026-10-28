# Istio Service Mesh & Zero-Trust Traffic Management (Lab 10)

[![Istio](https://img.shields.io/badge/Service%20Mesh-Istio%20v1.22%2B-466BB0?logo=istio)](https://istio.io/)
[![Zero Trust](https://img.shields.io/badge/Security-STRICT_mTLS-red)](#)
[![Traffic](https://img.shields.io/badge/Traffic-90%2F10_Canary_Splitting-blue)](#)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

An enterprise-grade Zero-Trust Service Mesh implementation on Kubernetes using Istio. Enforces end-to-end cryptographic pod-to-pod identity (SPIFFE/mTLS), fine-grained Layer 7 authorization policies (Deny-All by default), and automated Canary traffic shifting.

---

## 🌟 Security Architecture

- **STRICT Mutual TLS (mTLS):** Rejects all unencrypted plaintext traffic inside the cluster namespace via `PeerAuthentication`.
- **Zero-Trust Default Deny:** Replaces perimeter-only firewalls with pod-level `AuthorizationPolicy` requiring explicit service account identity matching (`principals: ["cluster.local/..."]`).
- **Path & Method Scoping:** Enforces least-privilege HTTP access bounded to specific paths (`/api/v1/*`) and HTTP verbs (`GET`, `POST`).
- **Canary 90/10 Traffic Splitting:** Shifts traffic safely between microservice versions (`v1` vs `v2`) with weighted `VirtualService` routes.

---

## 🚀 Quickstart

```bash
# Enable automatic Istio sidecar injection
kubectl label namespace production istio-injection=enabled

# Apply Zero-Trust Security & Canary Routing
kubectl apply -f istio-manifests/mesh-security.yaml

# Verify mTLS enforcement
istioctl authn tls-check <pod-name>.production
```

---

## 👤 Author
- **Engineer:** Rahul Motvani (DevOps / SRE / DevSecOps)
- **GitHub:** [github.com/rahulmotvani0-sketch](https://github.com/rahulmotvani0-sketch)
