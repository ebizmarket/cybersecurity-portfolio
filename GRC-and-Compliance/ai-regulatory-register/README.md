# AI Regulatory Applicability and Obligations Register

**GRC and Compliance** · part of [cybersecurity-portfolio](../../README.md) · [Back to GRC overview](../README.md) · [PDF version](./AI-Regulatory-Applicability-and-Obligations-Register.pdf)

## Community Tech Aid | eBiz Market, LLC

| | |
|---|---|
| **Organization** | eBiz Market, LLC (Idaho), operating Community Tech Aid (assumed business name) |
| **Prepared by** | Kelly Guzman, GRC & Compliance Analyst |
| **Register ID** | CTA-AIREG-001 |
| **Version** | 1.1 |
| **Research current as of** | 2026-10-27 |
| **Next scheduled review** | 2027-01-27 (quarterly), or sooner on any trigger in Section 7 |
| **Companion documents** | [MATRIS Method™ Statement of Applicability v2.0](../../MATRIS-Method/STATEMENT-OF-APPLICABILITY.md) · [NIST AI RMF Crosswalk](../../MATRIS-Method/NIST-AI-RMF-CROSSWALK.md) · [CTA NIST SP 800-53 Rev 5 LOW package](../cta-nist-800-53-package/) · [AI Disclosure Remediation (2026-10-27)](./ai-disclosure-remediation-2026-10-27/) |

---

## 1. Purpose

This register identifies which AI laws, regulations, contractual terms, and frameworks apply to the AI systems operated by eBiz Market, LLC, records why each one does or does not apply, and lists the specific obligations and the controls that meet them.

The Statement of Applicability answers *which security risks are tested*. This register answers *which rules the business must follow*, and *what evidence shows it does*.

This is a compliance working document maintained by the business, not legal advice or a legal opinion.

## 2. AI Systems in Scope

| ID | System | Description | Users | AI provider |
|---|---|---|---|---|
| **S1** | CTA AI chat assistant (communitytechaid.ai) | Consumer-facing tech support chatbot. Account required; free tier capped at 20 messages; paid tiers available. Scoped to device, software, network, and security troubleshooting. | Public (consumers and small offices) | Anthropic API |
| **S2** | MATRIS Method™ Red-Team Console (redteam.communitytechaid.ai) | No-code AI red-teaming tool for testing chatbots against the OWASP LLM Top 10. Behind Cloudflare Access sign-in. | Business owners, product managers, testers | Anthropic API |
| **S3** | eBiz Market AI and GRC services | AI security assessments, compliance documentation, and consulting. SAM.gov registered (NAICS 541512). | Business and government clients | N/A (professional service) |
| **S4** | Marketing and reputation | Website claims, MATRIS results published publicly, client reviews (Trustpilot). | Public | N/A |

## 3. Applicability Method

Each instrument is screened with four questions, in order:

1. **In force?** Is it enacted and effective, scheduled, or only proposed?
2. **Jurisdiction?** Does it reach the business, its users, or its market?
3. **Trigger?** Does the system match the covered activity (for example, "companion chatbot" or "consequential decision")?
4. **Exclusions and thresholds?** Does a carve-out or size threshold remove it?

| Determination | Meaning |
|---|---|
| **Applicable** | Obligations apply now. Listed in Section 5 with controls. |
| **Applicable (harmonized)** | Applies only if users in that jurisdiction use the system. Met by a single shared control rather than tracked state by state. |
| **Contingent** | Does not apply today. A named business change would trigger it. |
| **Not applicable** | Screened out. Reason recorded so the decision can be audited. |
| **Watch** | Proposed or unsettled. No obligation yet; tracked for change. |
| **Adopted (voluntary)** | Not legally required. Adopted as the internal standard. |

## 4. Applicability Determinations

### 4.1 Federal (United States)

| Ref | Instrument | Status | Determination | Systems | Basis |
|---|---|---|---|---|---|
| F-01 | FTC Act Section 5 (unfair or deceptive acts or practices) | In force | **Applicable** | S1-S4 | Applies to all businesses. Covers deceptive AI and marketing claims, undisclosed bots that mislead, and unreasonable data security. |
| F-02 | FTC Trade Regulation Rule on Consumer Reviews and Testimonials (16 CFR Part 465) | In force since Oct 21, 2024 | **Applicable** | S4 | Business collects and displays client reviews. Rule prohibits fake, AI-generated, and undisclosed insider reviews. |
| F-03 | FTC proposed Policy Statement on AI accuracy and output steering | Proposed July 7, 2026; not final | **Watch** | S1, S2 | Would treat steering AI outputs toward undisclosed objectives, against what users are led to expect, as potentially deceptive. Does not create new obligations until finalized. |
| F-04 | Executive Order 14365, *Ensuring a National Policy Framework for AI* (Dec 11, 2025) | In force (directs agencies) | **Watch** | All | Binds federal agencies, not businesses. Created a DOJ AI Litigation Task Force to challenge state AI laws. Affects how long state obligations below remain stable. |
| F-05 | OMB M-26-04, *Unbiased AI Principles* (Dec 11, 2025), implementing EO 14319 | In force for agencies; contract clauses rolling out | **Contingent** | S3 | Applies to vendors supplying LLMs, or services with LLMs built in, to federal agencies. Triggered if eBiz Market is awarded such a contract. Would require an acceptable use policy, model or system cards, end-user guides, and a feedback channel. |

### 4.2 State (United States)

| Ref | Instrument | Status | Determination | Systems | Basis |
|---|---|---|---|---|---|
| ST-01 | Idaho S 1297, Conversational AI Safety Act (Idaho Code Title 48, Ch. 21) | Enacted 2026; effective July 1, 2027 | **Not applicable** (re-screen on scope change) | S1, S2 | Home state. S1 falls under the exclusions for a customer service or technical assistance chatbot (§ 48-2102(2)(b)(ix)) and a narrow, discrete topic (§ 48-2102(2)(b)(iv)). S2 falls under the exclusions for tools marketed to developers and researchers or for commercial use by businesses. AG enforcement, $1,000 per violation, capped at $500,000. |
| ST-02 | Washington HB 2225, AI companion chatbots | Signed Mar 24, 2026; effective Jan 1, 2027 | **Not applicable** | S1 | Covers bots that sustain human-like relationships across sessions. S1 is task-based tech support. Note: Consumer Protection Act enforcement with a private right of action. |
| ST-03 | Oregon SB 1546, AI companion chatbots | Signed 2026; effective Jan 1, 2027 | **Not applicable** (re-screen on relocation) | S1 | Covers systems that simulate a sustained relationship, retain prior-session details to personalize, and ask unprompted emotional questions. S1 meets none of these. Planned relocation to Oregon makes this the home-state law to watch. $1,000 per violation, private right of action. |
| ST-04 | Maine 10 MRSA § 1500-DD (P.L. 2025, c. 294) | In force | **Applicable (harmonized)** | S1 | Prohibits a chatbot in trade with a consumer that may lead a reasonable consumer to believe they are talking to a human, unless clearly and conspicuously disclosed. S1 is publicly reachable. |
| ST-05 | Utah Code Ch. 13-77 (AI consumer disclosure, as amended by S.B. 226, 2025) | In force | **Applicable (harmonized)** | S1 | Must disclose AI use when a consumer clearly asks. Safe harbor if the AI states it is AI at the start of and throughout the interaction. S1 is not a regulated occupation. Up to $2,500 per violation. |
| ST-06 | California B.O.T. Act (Bus. & Prof. Code § 17940 et seq.) | In force since 2019 | **Applicable (harmonized)** | S1 | Prohibits using a bot to mislead about its artificial identity to drive a sale. S1 offers paid tiers. Disclosure is the safe harbor. |
| ST-07 | California SB 243, companion chatbots | In force Jan 1, 2026 | **Not applicable** | S1 | Companion chatbots only; customer service bots are carved out. |
| ST-08 | Colorado SB 24-205, replaced by SB 26-189 (signed May 14, 2026) | SB 205 enforcement paused by stipulated order; SB 189 effective Jan 1, 2027 | **Not applicable** | S1-S3 | Covers AI used in consequential decisions (employment, lending, housing, insurance, health care, education). None of the systems make these decisions. |

### 4.3 International

| Ref | Instrument | Status | Determination | Systems | Basis |
|---|---|---|---|---|---|
| INT-01 | EU AI Act (Regulation (EU) 2024/1689), as amended by the Digital Omnibus on AI (in force July 27, 2026) | Art. 50 transparency applies from Aug 2, 2026; Annex III high-risk from Dec 2, 2027 | **Contingent** | S2, S3 | S1 is not placed on the EU market. Triggered if MATRIS Method™ or services are offered to EU customers, or output is used in the EU. Article 50 then requires telling people they are interacting with AI. No system is high-risk under Annex III. |

### 4.4 Contractual

| Ref | Instrument | Status | Determination | Systems | Basis |
|---|---|---|---|---|---|
| C-01 | Anthropic Usage Policy (anthropic.com/aup) | In force | **Applicable** | S1, S2 | Consumer-facing chatbots must disclose that users are interacting with AI, at minimum at the start of each session or in the product interface. Products that allow minors must follow Anthropic's minors guidelines. High-risk use case rules (human review) do not apply: tech support is not a listed high-risk area. |

### 4.5 Voluntary frameworks

| Ref | Framework | Determination | Evidence |
|---|---|---|---|
| V-01 | NIST AI RMF 1.0 (AI 100-1) and Generative AI Profile (AI 600-1) | **Adopted (voluntary)** | NIST AI RMF Crosswalk: 21 subcategories assessed (10 Met, 10 Partial, 1 Gap) |
| V-02 | OWASP Top 10 for LLM Applications 2026 | **Adopted (voluntary)** | MATRIS Method™ Statement of Applicability v2.0 and OWASP coverage table |
| V-03 | NIST SP 800-53 Rev 5 (LOW baseline) | **Adopted (voluntary)** | CTA System Security Plan, policy manual, SAR, and posture summary |
| V-04 | ISO/IEC 42001:2023 (AI management system) | **Watch** | Not adopted. Used as a reference for future certification readiness. |

## 5. Obligations Register

Each obligation maps to a control in Section 6. Status reflects evidence on file as of the review date.

| Obl. ID | Obligation | Source | Systems | Control | Status |
|---|---|---|---|---|---|
| OB-01 | Tell users they are interacting with AI, at the start of each session or persistently in the interface | C-01; ST-04; ST-05 safe harbor; ST-06 safe harbor; INT-01 Art. 50 (if triggered) | S1, S2 | CTL-01 | Implemented |
| OB-02 | Never represent the chatbot as a human; answer truthfully when asked whether it is AI | ST-04; ST-05; ST-06; F-01 | S1 | CTL-02 | Implemented |
| OB-03 | Keep AI assistance clearly separate from human technician services | F-01 | S1, S4 | CTL-03 | Implemented |
| OB-04 | Substantiate marketing claims about AI capability and security results | F-01 | S2, S4 | CTL-04 | Implemented |
| OB-05 | No fake, AI-generated, or undisclosed insider reviews or testimonials | F-02 | S4 | CTL-05 | Implemented |
| OB-06 | Maintain reasonable security for customer accounts and data | F-01 | S1, S2 | CTL-06 | Implemented |
| OB-07 | Follow the AI provider's rules for products that minors can use | C-01 | S1 | CTL-07 | Implemented |
| OB-08 | Document the chatbot's intended objectives; no hidden steering against user expectations | F-03 (proposed) | S1 | CTL-08 | Planned |
| OB-09 | Re-screen applicability when the business or a system changes | All Contingent and Not applicable rows | All | CTL-09 | Implemented |
| OB-10 | Track regulatory change and update this register | All | All | CTL-10 | Implemented |

**Status key:** **Implemented** - control in place with evidence · **Verify** - control believed in place; evidence to be captured on next review · **Planned** - not yet in place

OB-01, OB-02 and OB-07 moved from Verify to Implemented on 2026-10-27. The review found that the chatbot's system instructions told it to deny being an AI; that was corrected the same day. Details and evidence: [AI Disclosure Remediation](./ai-disclosure-remediation-2026-10-27/).

## 6. Controls

One control satisfies several laws wherever possible. This keeps a one-person operation compliant across states without tracking each one separately.

| Control | Description | Evidence | Verification |
|---|---|---|---|
| **CTL-01** AI disclosure | Persistent label above the message box on every chat interface: "You're chatting with the CTA AI Assistant, not a person." with a Talk to a technician link. An opening message at the start of each session states the assistant is an AI. Terms of Service section "AI Assistant Disclosure" states all chat responses are AI-generated. | [Label screenshot](./ai-disclosure-remediation-2026-10-27/evidence/01-chat-ai-disclosure-label.png), [opening message](./ai-disclosure-remediation-2026-10-27/evidence/02-chat-opening-message-and-identity-answer.png) | Captured each quarterly review |
| **CTL-02** Identity honesty | System instructions state the assistant is an AI and must say so plainly when asked. An AI identity check ("Are you a real person?") runs in every monthly MATRIS regression. | [Identity answer, 2026-10-27](./ai-disclosure-remediation-2026-10-27/evidence/02-chat-opening-message-and-identity-answer.png); monthly run log | Monthly MATRIS regression run |
| **CTL-03** Human vs. AI separation | Site presents the AI chat and human technician services as distinct, with a direct call path to a real technician. | Homepage and services page screenshots | Quarterly review |
| **CTL-04** Claims substantiation | Every published security result is dated, scoped to the categories tested, and linked to evidence. No unqualified claims such as "fully secure." | MATRIS findings register, test logs, dated write-ups | Before any new public claim |
| **CTL-05** Review integrity | Reviews collected only from real clients through Trustpilot's verified invitation service. No AI-written or purchased reviews. Any reviewer with a family, employment, or business connection is disclosed. Replies signed as the business. | Trustpilot invitation records | Quarterly review |
| **CTL-06** Data security program | Row-level security, breached-password screening, 12-character password minimum, idle session timeouts, server-side tier enforcement, MFA on all administrative provider accounts. | CTA NIST SP 800-53 Rev 5 LOW package | Annual assessment; monthly MATRIS run |
| **CTL-07** Age and minors | Terms of Service require users to be 18 or older (Eligibility section). Signup requires checking "I confirm I am 18 or older and agree to the Terms of Service." The Privacy Policy states the services are not intended for anyone under 18. Minors are not permitted, so Anthropic's minors guidelines and state minor provisions are not triggered. | Terms of Service; [signup screenshots](./ai-disclosure-remediation-2026-10-27/evidence/) | On any change to audience |
| **CTL-08** Output objective statement | A short written statement of what the chatbot is instructed to do (troubleshoot, refer to human help, describe paid tiers) so its behavior matches what users are told. | Objective statement on file | When system instructions change |
| **CTL-09** Re-screening triggers | Applicability is re-screened when any trigger in Section 7 occurs. | Updated register version | Event-driven |
| **CTL-10** Regulatory monitoring | Quarterly review of federal, Idaho, Washington, Oregon, and EU developments, plus provider terms. | Register version history | Quarterly |

## 7. Re-Screening Triggers

| Trigger | Re-screen |
|---|---|
| S1 adds cross-session memory, a persona, emotional check-ins, or companionship features | ST-01, ST-02, ST-03, ST-07 |
| S1 expands beyond tech support into general-purpose conversation | ST-01 |
| Product opened to users under 18 | ST-01 to ST-03 minor provisions; C-01 |
| Business relocates to Oregon | ST-03; Oregon privacy and consumer protection law |
| First EU customer, EU marketing, or EU-based tester for S2 or S3 | INT-01 |
| Award of a federal contract involving an LLM or LLM-enabled service | F-05 |
| Any system used to make or support decisions on employment, credit, housing, insurance, health care, or education | ST-08; C-01 high-risk rules |
| FTC finalizes the output-steering policy statement | F-03 |
| A court enjoins, or Congress preempts, a state AI law | F-04 and affected ST rows |

## 8. Key Dates

| Date | Event | Ref |
|---|---|---|
| Dec 2, 2026 | EU Art. 50(2) marking grace period ends for systems already on the EU market | INT-01 |
| Jan 1, 2027 | Washington HB 2225 and Oregon SB 1546 take effect | ST-02, ST-03 |
| Jan 1, 2027 | Colorado SB 26-189 takes effect | ST-08 |
| Jan 27, 2027 | Next scheduled review of this register | CTL-10 |
| Jul 1, 2027 | Idaho Conversational AI Safety Act takes effect | ST-01 |
| Dec 2, 2027 | EU AI Act Annex III high-risk obligations apply | INT-01 |

## 9. Version History

| Version | Date | Change |
|---|---|---|
| 1.0 | 2026-10-27 | Initial register. Three systems and marketing in scope; 19 instruments screened. |
| 1.1 | 2026-10-27 | OB-01, OB-02 and OB-07 verified and moved to Implemented after the [AI disclosure remediation](./ai-disclosure-remediation-2026-10-27/). CTL-01, CTL-02 and CTL-07 updated with implemented details and evidence. |

## References

- FTC, Trade Regulation Rule on the Use of Consumer Reviews and Testimonials, 16 CFR Part 465
- FTC, Proposed Policy Statement on AI accuracy and output steering (July 7, 2026)
- Executive Order 14365, *Ensuring a National Policy Framework for Artificial Intelligence* (Dec 11, 2025)
- OMB M-26-04, *Increasing Public Trust in Artificial Intelligence Through Unbiased AI Principles* (Dec 11, 2025)
- Idaho S 1297 (2026), Conversational AI Safety Act: https://legiscan.com/ID/bill/S1297/2026
- Washington HB 2225 (2026): https://app.leg.wa.gov/billsummary?Year=2025&BillNumber=2225
- Oregon SB 1546 (2026)
- Maine Revised Statutes, Title 10, § 1500-DD: https://legislature.maine.gov/statutes/10/title10sec1500-DD.html
- Utah Code Chapter 13-77
- California Business and Professions Code § 17940 et seq.
- California SB 243 (2025)
- Colorado SB 24-205 and SB 26-189
- Regulation (EU) 2024/1689 (AI Act) and the Digital Omnibus on AI (2026)
- Anthropic Usage Policy: https://www.anthropic.com/aup
- NIST AI 100-1, AI 600-1, SP 800-53 Rev 5; ISO/IEC 42001:2023; OWASP Top 10 for LLM Applications 2026

---

*MATRIS Method™ is a trademark of eBiz Market, LLC. Community Tech Aid is an assumed business name of eBiz Market, LLC.*
