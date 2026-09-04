# 🌐 Awesome API Management Tools

![Status](https://img.shields.io/badge/Status-Active_Curation-brightgreen?style=for-the-badge&logo=github&logoColor=white)
![Maintainer](https://img.shields.io/badge/Maintainer-SunnyJayaRaju-orange?style=for-the-badge)

> **A personal, opinionated list of API management tools I've actually evaluated, used in production, or keep coming back to.**  
> This started as a fork of [mailtoharshit/Awesome-Api-Management-Tools](https://github.com/mailtoharshit/Awesome-Api-Management-Tools) — now maintained as my own curated reference.

---

## 🎯 Why This Exists

The original awesome list is exhaustive — 300+ tools across every category. That's great for discovery, terrible for decisions.  
I needed a shorter list: tools I've **touched**, **trust**, and **would recommend to a teammate**.

> **"If I've used it in anger (prod, staging, or a real eval), it's here. If not, it's not."**

---

## 🗂️ Table of Contents

- [🚪 API Gateways & Management Platforms](#-api-gateways--management-platforms)
- [📐 API Design & Specification](#-api-design--specification)
- [🧪 Testing & Debugging](#-testing--debugging)
- [🧹 Linting & Governance](#-linting--governance)
- [📚 Documentation & Portals](#-documentation--portals)
- [🔐 Security & Auth](#-security--auth)
- [📊 Monitoring & Observability](#-monitoring--observability)
- [⚙️ CLI & Automation](#%EF%B8%8F-cli--automation)
- [🔗 Connected Repos](#-connected-repos)

---

## 🚪 API Gateways & Management Platforms

| Tool | Category | My Take |
|------|----------|---------|
| **[Apigee / Apigee X](https://cloud.google.com/apigee)** | Enterprise API Platform | My daily driver. Proxy bundles, flow variables, KVMs, SpikeArrest/Quota — the mental model clicks. X adds better CI/CD and regional routing. |
| **[Kong](https://konghq.com/)** | Open-source Gateway | Solid plugin ecosystem. Used it for a side project; declarative config (deck) makes GitOps straightforward. |
| **[AWS API Gateway](https://aws.amazon.com/api-gateway/)** | Cloud-native Gateway | Great for serverless (Lambda, HTTP APIs). REST API mode shows its age — prefer HTTP API for cost/latency. |
| **[Traefik](https://traefik.io/)** | Edge Router / Ingress | Kubernetes-native, auto-discovers services. Used as ingress controller; Let's Encrypt integration is painless. |

---

## 📐 API Design & Specification

| Tool | Category | My Take |
|------|----------|---------|
| **[OpenAPI 3.x](https://spec.openapis.org/oas/v3.1.0)** | Spec Standard | The lingua franca. Write once, generate clients/docs/mocks/tests. Use **Spectral** for linting (see below). |
| **[Postman](https://www.postman.com/)** | Design + Client | Collection format is portable. Good for exploratory testing and sharing runnable examples with non-engineers. |
| **[Stoplight Studio](https://stoplight.io/open-source/studio)** | Visual Editor | Best visual OpenAPI editor I've found. Git-backed, renders beautifully, catches errors as you type. |
| **[Apigee API Hub](https://cloud.google.com/apigee/docs/api-hub/overview)** | Registry | Central catalog for specs, versions, deployments. Integrates with Apigee runtime — single source of truth. |

---

## 🧪 Testing & Debugging

| Tool | Category | My Take |
|------|----------|---------|
| **[Postman](https://www.postman.com/)** | Collection Runner | Collection runner + Newman CLI = CI-ready contract tests. Variables/environments make multi-env trivial. |
| **[HTTPie](https://httpie.io/)** | CLI Client | Human-readable output, sensible defaults. `http GET :8080/api/users` beats `curl -X GET ...` every time. |
| **[Mockoon](https://mockoon.com/)** | Desktop Mock Server | Zero-config local mocking. Import OpenAPI, tweak responses, proxy to real backend for partial mocks. |
| **[Reqres](https://reqres.in/)** | Hosted Sandbox | Quick smoke tests when you need a live endpoint *now*. No auth, no setup. |

---

## 🧹 Linting & Governance

| Tool | Category | My Take |
|------|----------|---------|
| **[Spectral](https://meta.stoplight.io/spectral/)** | OpenAPI Linter | Extensible ruleset (OOTB: OpenAPI 3.0/3.1, asyncAPI). Runs in CI, outputs SARIF for GitHub code scanning. |
| **[apigeelint](https://github.com/apigee/apigeelint)** | Apigee Bundle Linter | **Essential for Apigee.** Catches proxy anti-patterns (missing fault rules, hardcoded URLs, unused variables) before deploy. |
| **[Vacuum](https://github.com/daveshanley/vacuum)** | Fast OpenAPI Linter | Go-based, blazing fast. Good Spectral alternative if you want zero Node deps. |

---

## 📚 Documentation & Portals

| Tool | Category | My Take |
|------|----------|---------|
| **[Redoc](https://redocly.github.io/redoc/)** | Reference Docs | Clean, three-panel output from OpenAPI. Customizable theming, search, code samples in 10+ languages. |
| **[Redocly CLI](https://redocly.com/docs/cli/)** | Docs Pipeline | Bundle multi-file specs, lint, preview, deploy. The `preview-docs` command is my local feedback loop. |
| **[Apigee Developer Portal (Drupal / Integrated)](https://cloud.google.com/apigee/docs/api-platform/publish/overview)** | Full Portal | If you're on Apigee, the integrated portal saves wiring. Custom domains, auth, monetization baked in. |
| **[Slate](https://github.com/slatedocs/slate)** | Static Docs | Markdown-driven, three-column layout. Used for internal API guides — versioned in repo, deployed via Pages. |

---

## 🔐 Security & Auth

| Tool | Category | My Take |
|------|----------|---------|
| **[OAuth 2.0 / OIDC](https://oauth.net/2/)** | Auth Standard | Authorization Code + PKCE for SPAs, Client Credentials for M2M. Apigee's `OAuthV2` policy handles token gen/validation natively. |
| **[JWT](https://jwt.io/)** | Token Format | Stateless auth. Validate `exp`, `iss`, `aud` in gateway (Apigee `VerifyJWT` policy) — don't forward to backend. |
| **[mTLS](https://en.wikipedia.org/wiki/Mutual_authentication)** | Transport Security | Service-to-service trust. Apigee `TargetEndpoint` `SSLInfo` + KVM certs = zero-trust between proxy and backend. |
| **[OWASP ZAP](https://www.zaproxy.org/)** | Security Scanner | CI-integrated DAST. Active scan finds injection, broken auth, sensitive data exposure. Baseline scan on every PR. |

---

## 📊 Monitoring & Observability

| Tool | Category | My Take |
|------|----------|---------|
| **[Apigee Analytics](https://cloud.google.com/apigee/docs/api-platform/analytics/overview)** | Built-in Analytics | Latency percentiles, error rates, developer engagement. Good for exec dashboards; limited cardinality for deep debugging. |
| **[Prometheus + Grafana](https://prometheus.io/)** | Metrics Stack | Standard for custom metrics. Scrape Apigee via `apigee-exporter` or push from backend. |
| **[OpenTelemetry](https://opentelemetry.io/)** | Traces/Logs/Metrics | Vendor-neutral instrumentation. Export to Tempo/Jaeger, Loki, Prometheus. Future-proofs observability. |
| **[Moesif](https://www.moesif.com/)** | API Analytics SaaS | User-centric (not request-centric). Funnel analysis, retention cohorts, alerting on business metrics. |

---

## ⚙️ CLI & Automation

| Tool | Category | My Take |
|------|----------|---------|
| **[apigeecli](https://github.com/apigee/apigeecli)** | Apigee CLI | Deploy proxies, manage envs, KVMs, developers, products — all from terminal. Replaces `apigeetool` and `maven` plugin. |
| **[deck](https://deck.konghq.com/)** | Kong Declarative Config | `deck sync` = GitOps for Kong. Diff before apply, backup/restore, drift detection. |
| **[Newman](https://github.com/postmanlabs/newman)** | Postman CLI | Run collections in CI. `newman run collection.json -e env.json --reporters cli,junit` → JUnit XML for pipeline gates. |
| **[jq](https://stedolan.github.io/jq/)** | JSON Processor | `curl ... | jq '.data[] | select(.status=="active")'` — the universal API data knife. |

---

## 🔗 Connected Repos

This list lives alongside my hands-on work:

| Repo | Purpose |
|------|---------|
| **[Apigee-Lab](https://github.com/SunnyJayaRaju/Apigee-Lab)** | Production-style Apigee proxies (JWT, Caching, FaultRules, ServiceCallouts) |
| **[Curious-Explorer](https://github.com/SunnyJayaRaju/Curious-Explorer)** | Concept index: "Waiter vs Kitchen" (proxies), "Hotel Key Card" (OAuth), "Bouncer vs Bartender" (SpikeArrest vs Quota) |

---

## 🧭 How I Evaluate Tools

1. **Does it solve a real problem I have?** (Not "cool tech")
2. **Can I run it locally / in CI?** (No SaaS-only black boxes for core workflows)
3. **Is the mental model learnable in an afternoon?** (If not, it's a liability)
4. **Does it play nice with GitOps?** (Declarative config, drift detection, PR-based changes)
5. **Would I debug it at 2 AM?** (Good logs, clear errors, escape hatches)

---

## 📝 Changelog

- **2026-09-04** — Initial rewrite: fork → personal curated list. Trimmed 300+ entries to ~40 tools I've actually used.

---

## 🙏 Attribution

Original list © 2018+ [Harshit Pandey](https://github.com/mailtoharshit) (MIT).  
This curated version © 2025 [SunnyJayaRaju](https://github.com/SunnyJayaRaju) — same license, new voice.

> *Curated with 🧠 by someone who learns by breaking things in staging first.*