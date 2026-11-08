# George Mareev

### AI Engineer — self-hosted LLM platforms with controlled model access

I build self-hosted enterprise AI platforms: model gateways, production RAG assistants, secure
deployment, evaluation, observability and prompt-level audit. Model and embedding endpoints can be
local or OpenAI-compatible services; data residency depends on the configured endpoints.

[Portfolio](https://mareevapps.com/) · [Runnable public reference](https://github.com/GoshaMareev/secure-llm-platform-reference)

---

## What I've built

**Self-hosted AI platform for an enterprise customer** — designed and delivered end to end, running in production.

**Gateway & infrastructure**
LiteLLM as the single model gateway, Open WebUI as the user surface, PostgreSQL, nginx with TLS
termination, SSO through Microsoft Entra ID. Four services deployed and operated independently, with
the public surface limited to the ingress and everything else bound to loopback. Separate databases and
database users per service. Documented handling of corporate egress proxies at both the container
runtime and image registry layers.

**RAG agents**
Two production assistants on a shared core. Metadata-aware retrieval over `doc_category` / `system` /
`audience` / `topic_tags`, glossary-driven query expansion, keyword overlap on top of vector scores,
reranking with a fallback when reranking degrades context, confidence scoring with grounded refusal
instead of hallucination, and a feedback loop that feeds back into ranking. Pluggable embedding
backends — Ollama, local HuggingFace, or a remote OpenAI-compatible service with batching and
in-app normalization. Multi-format document indexing with incremental and full rebuild modes,
manifest tracking, and a multimodal fallback for PDFs without a text layer. SharePoint sync via
Microsoft Graph with versioning and clickable source attribution.

**Agent orchestration & guardrails**
Dify for agent composition and guardrail policy on the platform layer, so policy lives above the
individual application rather than inside it. *(In progress.)*

**Observability & security audit**
Fluent Bit shipping container logs from journald to Grafana Loki over RFC5424 syslog, plus a separate
audit stream to SIEM for prompt-level control. The two streams never intersect by design — prompts do
not pass through journald and therefore never reach the operational log store. Unprivileged container:
non-root user, `cap_drop: ALL`, `no-new-privileges`, read-only root filesystem, journal mounted
read-only. Credential masking in Lua, filesystem-backed queues with disk-resident emitter buffers,
Prometheus metrics. Shipped with a SIEM audit field reference and a detection-rule roadmap covering
IAM events, prompt-injection verdicts, guardrail blocks, and audit delivery control.

**Quality & operations**
A/B comparison harness for two agent deployments measuring latency, confidence and source counts;
expert QA review workflow with spreadsheet round-trips; k6 load tests; GitLab CI; systemd units;
deployment runbooks and an operations cheatsheet.

Most of this work lives in private repositories. Happy to walk through the architecture, the trade-offs,
and what broke along the way.

---

## What I work on

- **LLM gateways and on-prem inference** — LiteLLM, Ollama, OpenAI-compatible endpoints, quantized serving
- **Retrieval quality** — metadata-aware ranking, reranking, glossaries, scope detection, grounded refusal
- **Evaluation** — A/B agent comparison, confidence calibration, expert review loops, regression tracking
- **Guardrails and AI safety** — prompt-injection hardening, boundary validation, PII-aware handling, policy enforcement at the platform layer
- **Observability and audit** — structured logging, Loki, prompt audit to SIEM, detection rules
- **Secure deployment** — SSO and identity proxying, least-privilege containers, environment isolation, secrets hygiene

## Currently

- Guardrail policy and agent composition in Dify
- Prompt audit to SIEM: detection rules for injection attempts and policy violations
- TLS for the audit channel
- Warmup and concurrency control for on-prem inference under load

## Open to

AI engineering, LLM infrastructure and LLMOps roles, with a focus on controlled model access,
retrieval quality and reliable operations in data-sensitive environments.

---

## Stack

**Built and operated in production**
Python · Flask · LiteLLM · Open WebUI · Dify · Ollama · OpenAI-compatible inference & embedding endpoints ·
ChromaDB · rerankers · PostgreSQL · SQLite · Docker & Compose · nginx · systemd · Linux ·
oauth2-proxy & Microsoft Entra ID · Microsoft Graph · Fluent Bit · Grafana Loki · Lua · k6 · GitLab CI · Bash

**Also worked with**
FastAPI · Pydantic · HuggingFace · FAISS · PyTorch · scikit-learn · NumPy · Pandas · Apache Spark ·
SQL · Matplotlib · Plotly

---

## Connect

- Portfolio — [mareevapps.com](https://mareevapps.com)

