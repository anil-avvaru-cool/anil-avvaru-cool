# Anil Kumar Avvaru

AI/ML platform engineer — building production-grade intelligent insurance systems.

---

## Featured project — Redwood AI Insurance Platform

End-to-end intelligent insurance operations platform spanning the full lifecycle — from quote generation through claims settlement — via risk scoring, real-time fraud detection, and autonomous claims automation.

The platform is built on a shared data spine: the underwriting risk score is stored at quote time and re-enters fraud detection as a feature at FNOL time. Without this, a high-risk policy filed shortly after issuance — one of the strongest fraud signals in personal auto — is invisible to the claims model.

→ **[redwood-ai-insurance](https://github.com/anil-avvaru-cool/redwood-ai-insurance)** (umbrella repo — start here)

### Platform repos

| Repo | Focus | Status |
|---|---|---|
| [insurance-data-platform](https://github.com/anil-avvaru-cool/insurance-data-platform) | Entity resolution, feature store, synthetic data generation | ✅ Complete |
| [ai-fraud-detection-platform](https://github.com/anil-avvaru-cool/ai-fraud-detection-platform) | Ensemble fraud scoring, graph intelligence, sync/async inference | ✅ Complete |
| [intelligent-underwriting-platform](https://github.com/anil-avvaru-cool/intelligent-underwriting-platform) | Two-stage hurdle model, quote generation agent | ✅ Complete |
| [fnol-claims-multi-agent-system](https://github.com/anil-avvaru-cool/fnol-claims-multi-agent-system) | FNOL Agent, document verification, investigator copilot | 📋 Planned — Week 5 |
| [enterprise-rag-platform](https://github.com/anil-avvaru-cool/enterprise-rag-platform) | Reusable RAG library consumed by underwriting and claims agents | ✅ Complete |

### Key architectural decisions

What makes this platform different from a collection of ML models is the reasoning behind every design choice. Selected decisions from the [Decision Log](https://github.com/anil-avvaru-cool/redwood-ai-insurance/blob/main/docs/DECISION_LOG.md):

- **DEC-001** — Telematics nulls are `null`, never imputed. XGBoost learns the adverse selection signal from the 60% of non-telematics users directly. Imputing a neutral midpoint masks it.
- **DEC-004** — `feature_definitions.py` is Layer 0. Archetypes import from it; it imports from nothing. This prevents training-serving skew from the first line of code.
- **DEC-010** — `risk_score_at_issuance` is stored in the feature store at quote time and re-read as a fraud feature at FNOL time. This is the shared data spine.
- **DEC-011** — Entity resolution runs before graph construction. A `shares_address` edge between two unnormalized strings degrades Louvain community detection silently — fraud rings appear disconnected.

### Technology highlights

- **Fraud ensemble:** XGBoost + GraphSAGE + NLP transformer + ViT → stacking meta-learner → SHAP per-decision explainability
- **Inference:** hybrid sync (<100ms, blocks FNOL submission) + async (deep enrichment — full graph traversal, LLM narrative reconciliation, third-party enrichment)
- **Label quality:** PU learning + Confident Learning (cleanlab) + delayed confirmed-label pipeline keyed on `fraud_confirmed_at`
- **Graph intelligence:** Neo4j fraud ring detection via Louvain community detection, attorney/body-shop centrality scoring, coordinated submission burst detection
- **Drift monitoring:** PSI current-period window keyed on event-time anchors (`fnol_submitted_at`, `quote_requested_at`) — not feature store freeze time

---

## Core technologies

**AI & ML** — Agentic AI · LLM · RAG · Vector embeddings · XGBoost · LightGBM · Graph neural networks (GraphSAGE) · SHAP

**Data infrastructure** — Databricks · Kafka · Redis · Neo4j / Amazon Neptune · Apache Spark · Feature stores · Parquet

**Cloud & platform** — AWS · Azure · GCP · Kubernetes · Docker · Terraform · Bicep

**Engineering** — Event-driven architecture · Domain-driven design · .NET Core 10 · React 18 · FastAPI · OAuth2

---

## Certifications

- AWS Certified Generative AI Developer – Professional
- Microsoft Azure Solutions Architect Expert
- Certified Kubernetes Administrator (CKA)
- Certified Kubernetes Application Developer (CKAD)

---

## Writing

- **[Your fraud labels are lying to you](https://anilavvaru.substack.com/p/your-fraud-labels-are-lying-to-you)** — why PU learning matters for insurance ML (Substack)
- *How we built a sub-100ms fraud scorer on AWS* — in progress, Towards Data Science
- *What C-suite gets wrong about claims AI* — in progress

---

*Stack: Python · XGBoost · Neo4j · Redis · FastAPI · AWS | Active development: 2026 Q2*

<!--
**anil-avvaru-cool/anil-avvaru-cool** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
