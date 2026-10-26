# MATRIS Method™ - NIST AI RMF Crosswalk

**MATRIS Method™** · part of [cybersecurity-portfolio](../README.md) · [Methodology](./METHODOLOGY.md) · [Back to MATRIS overview](./README.md)

| | |
|---|---|
| **Frameworks** | NIST AI 100-1, AI Risk Management Framework 1.0 · NIST AI 600-1, Generative AI Profile |
| **System in scope** | Community Tech Aid chatbot (`communitytechaid.ai/chat`), tested with MATRIS Red-Team Console BETA v1 |
| **Date** | October 26, 2026 |
| **Prepared by** | Kelly Guzman |

This crosswalk shows where MATRIS Method™ activities produce evidence for AI RMF outcomes, and where they do not. It is a self-assessment against selected subcategories, not a claim of AI RMF conformance. Subcategory descriptions are paraphrased; see NIST AI 100-1 for the full text.

**Status key:** **Met** - evidence exists in this repository · **Partial** - some evidence, gap stated · **Gap** - not addressed yet

---

## Where MATRIS fits

MATRIS is primarily a **MEASURE** activity: it tests a deployed chatbot against defined risks and records the result. Its methodology and verdict criteria support **GOVERN** and **MAP**, and its findings and severity ratings feed **MANAGE**.

```
 GOVERN   Published method, verdict criteria, evidence standard
   |
 MAP      Target context (who uses the bot) -> tailored test library -> OWASP LLM mapping
   |
 MEASURE  MATRIS test rounds -> human-confirmed PASS / WARN / FAIL -> JSON evidence
   |
 MANAGE   Findings rated by likelihood x impact -> prioritized fixes -> retest
```

---

## GOVERN

| ID | Outcome (paraphrased) | MATRIS / CTA evidence | Status |
|---|---|---|:---:|
| GOVERN 1.4 | Risk management process and outcomes are set out in transparent policies and procedures | [Methodology](./METHODOLOGY.md): procedure, verdict criteria, evidence standard, published limitations | **Met** |
| GOVERN 1.5 | Ongoing monitoring and periodic review are planned, with roles and frequency defined | Retest after any model, prompt or setting change is stated as policy. No fixed retest schedule. | **Partial** |
| GOVERN 2.1 | Roles, responsibilities and lines of communication for AI risk are documented | Operator selects tests and confirms every verdict. One-person operation: builder, tester and reviewer are the same person (disclosed). | **Partial** |
| GOVERN 4.3 | Practices are in place to enable AI testing, incident identification and information sharing | MATRIS console in use; Round 01 results and operational observation OBS-01 published | **Met** |
| GOVERN 6.1 | AI risks from third parties are addressed | The chatbot runs on a third-party model. MATRIS tests the deployed behavior regardless of provider. No provider attestations on file. | **Partial** |

## MAP

| ID | Outcome (paraphrased) | MATRIS / CTA evidence | Status |
|---|---|---|:---:|
| MAP 1.1 | Intended purpose, users and context of use are understood and documented | Target serves non-technical users, including seniors. The test library includes two scam-specific categories for that reason ([Methodology §3](./METHODOLOGY.md#3-test-library-beta-v1)). | **Met** |
| MAP 1.5 | Organizational risk tolerances are determined and documented | Verdict criteria define what counts as PASS, WARN and FAIL. Console scoring does not yet treat a FAIL as a stop condition. | **Partial** |
| MAP 2.2 | System knowledge limits and human oversight of outputs are documented | Drift check: bot declined an out-of-scope speed test instead of inventing results. Every verdict is human-confirmed. | **Partial** |
| MAP 5.1 | Likelihood and magnitude of identified impacts are documented | [Finding severity matrix](./METHODOLOGY.md#8-finding-severity): likelihood x impact, with compensating-control rule | **Met** |

## MEASURE

| ID | Outcome (paraphrased) | MATRIS / CTA evidence | Status |
|---|---|---|:---:|
| MEASURE 1.1 | Approaches and metrics are selected for the mapped risks; unmeasured risks are documented | Seven tests mapped to OWASP LLM categories; PASS/WARN/FAIL plus session score. The five untested OWASP categories are listed as Planned. | **Met** |
| MEASURE 1.3 | Internal experts who were not front-line developers, or independent assessors, are involved in assessments | Not met. Same person built the system, the tool and the tests. Disclosed in every report. | **Gap** |
| MEASURE 2.1 | Test sets, metrics and tool details are documented | [Methodology](./METHODOLOGY.md) plus raw [JSON log](./matris-redteam-test-2026-08-27/matris-test-log.json) with verbatim payloads and responses | **Met** |
| MEASURE 2.6 | The system is evaluated regularly for safety risks | Two consumer-harm tests (scam validation, in-progress scam) passed on 2026-08-27. One round so far, not yet regular. | **Partial** |
| MEASURE 2.7 | Security and resilience are evaluated and documented | [Round 01](./matris-redteam-test-2026-08-27/): prompt injection, jailbreak, system prompt leakage, excessive agency, all PASS | **Met** |
| MEASURE 2.10 | Privacy risk is examined and documented | Sensitive information disclosure test passed. Automated screening coverage for secrets is limited (console self-assessment, publication pending). | **Partial** |
| MEASURE 3.1 | Existing, unanticipated and emergent risks are identified and tracked | Observation OBS-01 logged; console self-assessment drafted. No standing risk register yet. | **Partial** |

## MANAGE

| ID | Outcome (paraphrased) | MATRIS / CTA evidence | Status |
|---|---|---|:---:|
| MANAGE 1.2 | Treatment of documented risks is prioritized by impact and likelihood | Findings rated with the [severity matrix](./METHODOLOGY.md#8-finding-severity); fix order follows severity | **Met** |
| MANAGE 1.3 | Responses to high-priority risks are planned and documented | Recommendations written for each console finding. Fixes not yet implemented. | **Partial** |
| MANAGE 1.4 | Residual risks are documented | Round 01 limitations state untested categories, single-turn scope and manual capture | **Partial** |
| MANAGE 4.1 | Post-deployment monitoring plans are implemented | No continuous monitoring. Testing is periodic and manual. | **Gap** |
| MANAGE 4.3 | Incidents and errors are communicated to relevant parties | Observations and findings are published in this repository | **Partial** |

---

## Generative AI Profile (NIST AI 600-1)

How each MATRIS test category lines up with the generative AI risks in the GAI Profile.

| MATRIS test | OWASP LLM | Closest GAI risk |
|---|---|---|
| System Prompt Leak | LLM07 | Information Security |
| Direct Prompt Injection | LLM01 | Information Security |
| Roleplay Jailbreak | LLM01 | Information Security; Dangerous, Violent, or Hateful Content |
| Sensitive Info Disclosure | LLM02 | Data Privacy; Information Security |
| Excessive Agency | LLM06 | Information Security; Human-AI Configuration |
| Scam Validation Failure | LLM09 | Information Integrity; Human-AI Configuration |
| In-Progress Scam Assistance | LLM09 | Information Integrity; Human-AI Configuration |
| Drift and hallucination check | LLM09 | Confabulation |

---

## Summary

| Function | Met | Partial | Gap |
|---|:---:|:---:|:---:|
| GOVERN | 2 | 3 | 0 |
| MAP | 2 | 2 | 0 |
| MEASURE | 3 | 3 | 1 |
| MANAGE | 1 | 3 | 1 |
| **Total (21)** | **8** | **11** | **2** |

**Strongest:** MEASURE. MATRIS produces documented, reproducible security and safety test evidence against a live system.

**Weakest:** independence (MEASURE 1.3) and continuous monitoring (MANAGE 4.1). Both are structural for a one-person operation. The practical closes are an outside reviewer for a future round, and a fixed retest schedule tied to chatbot changes.

## References

- [NIST AI 100-1, Artificial Intelligence Risk Management Framework (AI RMF 1.0)](https://doi.org/10.6028/NIST.AI.100-1)
- [NIST AI 600-1, Generative Artificial Intelligence Profile](https://doi.org/10.6028/NIST.AI.600-1)
- [OWASP Top 10 for LLM Applications](https://genai.owasp.org/)
