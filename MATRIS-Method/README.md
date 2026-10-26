# MATRIS Method™ - Zero-Code LLM Red-Teaming & Security Audit Framework

[![OWASP GenAI Solutions Directory](https://img.shields.io/badge/OWASP%20GenAI-Solutions%20Directory-000000?style=flat-square)](https://genai.owasp.org/solution/matris-method-red-team-console/)
[![SaaSHub Listed](https://cdn-b.saashub.com/img/badges/approved-color.png?v=1)](https://www.saashub.com/matris-method-by-community-tech-aid)
![Security+ Certified](https://img.shields.io/badge/CompTIA-Security%2B-007ACC?style=flat-square&logo=comptia&logoColor=white)
![OWASP LLM Top 10](https://img.shields.io/badge/OWASP-LLM%20Top%2010-FF5722?style=flat-square)
![Audit Coverage](https://img.shields.io/badge/Framework-Zero--Code%20Red--Teaming-success?style=flat-square)
![Status](https://img.shields.io/badge/Verification-Production--Verified-brightgreen?style=flat-square)

> **Author:** Kelly Guzman | [Live Verification & Evidence](https://communitytechaid.ai/red-team) | [Email Contact](mailto:contact@ebizmarket.net)

---

### Executive Overview

The **MATRIS Method™** is a structured, zero-code red-teaming and compliance auditing methodology engineered to test, validate, and document generative AI safety boundaries before enterprise deployment. 

Mapped directly to the **OWASP Top 10 for Large Language Model Applications**, MATRIS provides both security engineers and non-technical stakeholders with reproducible testing vectors, human-confirmed verdicts, and a standardized risk scorecard.

### Documentation

| Page | What it covers |
| :--- | :--- |
| [OWASP GenAI Solutions Directory listing](https://genai.owasp.org/solution/matris-method-red-team-console/) | Independent listing by the OWASP GenAI Security Project (October 4, 2026) |
| [Methodology](./METHODOLOGY.md) | Inspection layers, test library, procedure, verdict criteria, screening, scoring, evidence standard, limitations |
| [Console Self-Assessment (2026-10-25)](./console-self-assessment-2026-10-25/) | MATRIS tested itself: 6 findings in the console's screening and scoring, with reproduction script |
| [Findings Register](./FINDINGS.md) | Every finding and observation, with severity, status and closure |
| [Monitoring Plan](./MONITORING-PLAN.md) | Monthly regression and access review, change-triggered retests, independent review plan, run log |
| [NIST AI RMF Crosswalk](./NIST-AI-RMF-CROSSWALK.md) | MATRIS mapped to AI RMF 1.0 subcategories and the NIST Generative AI Profile, with gaps marked |
| [Test Round 01 (2026-08-27)](./matris-redteam-test-2026-08-27/) | Live test of the Community Tech Aid chatbot: results, evidence, observations |
| [LinkedIn article](https://www.linkedin.com/pulse/ai-security-tools-assume-you-have-dev-team-i-dont-one-kelly-guzman-kdb6c/) | Why MATRIS exists and what the first round showed |

---

### OWASP Top 10 for LLMs - MATRIS Coverage Matrix

| OWASP ID | Vulnerability Classification | MATRIS Testing Vector / Attack Surface | Status | Evidence |
| :--- | :--- | :--- | :---: | :--- |
| **LLM01** | Prompt Injection | Direct prompt injection, roleplay jailbreak | Tested 2026-08-27 · Pass 2/2 | [2026-08-27 evidence](./matris-redteam-test-2026-08-27/) |
| **LLM02** | Sensitive Info Disclosure | Sensitive information elicitation, system boundary probing | Tested 2026-08-27 · Pass 1/1 | [2026-08-27 evidence](./matris-redteam-test-2026-08-27/) |
| **LLM03** | Supply Chain Weaknesses | Third-party plugin abuse, unvetted external dependency mapping | Planned | - |
| **LLM04** | Data & Model Poisoning | Context poisoning, grounding data bias induction, adversarial in-context injection | Planned | - |
| **LLM05** | Improper Output Handling | Stored XSS generation via Markdown/HTML, downstream SSRF payload reflection | Planned | - |
| **LLM06** | Excessive Agency | Unvalidated action and transaction requests | Tested 2026-08-27 · Pass 1/1 | [2026-08-27 evidence](./matris-redteam-test-2026-08-27/) |
| **LLM07** | System Prompt Leakage | System prompt exfiltration attempt | Tested 2026-08-27 · Pass 1/1 | [2026-08-27 evidence](./matris-redteam-test-2026-08-27/) |
| **LLM08** | Vector & Embedding Weakness | Context retrieval poisoning, vector search delimiter bypass, injection via RAG | Planned | - |
| **LLM09** | Misinformation / Hallucination | In-progress scam assistance, scam validation pressure | Tested 2026-08-27 · Pass 2/2 | [2026-08-27 evidence](./matris-redteam-test-2026-08-27/) |
| **LLM10** | Unbounded Consumption | DoS payload recursion, token exhaustion prompts, state memory inflation | Planned | - |