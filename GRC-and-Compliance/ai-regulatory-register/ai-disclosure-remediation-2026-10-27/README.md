# AI Disclosure Remediation: Community Tech Aid Chatbot

**GRC and Compliance** · part of [cybersecurity-portfolio](../../../README.md) · [AI Regulatory Register](../README.md) · [Back to GRC overview](../../README.md)

| | |
|---|---|
| **System** | Community Tech Aid AI chat assistant (`communitytechaid.ai`, `/chat` and `/triage`) |
| **Date** | 2026-10-27 (found, fixed and verified the same day) |
| **Prepared by** | Kelly Guzman, GRC & Compliance Analyst |
| **Triggered by** | Verification of OB-01, OB-02 and OB-07 in the [AI Regulatory Applicability and Obligations Register](../README.md) |
| **Result** | 3 findings closed, 1 open (Low) |

---

## Summary

The new AI regulatory register marked three obligations "Verify": tell users they are talking to an AI, never claim to be human, and set a minimum user age. Checking them turned up a bigger problem than a missing label. The chatbot's own system instructions told it that it was **not** an AI.

That instruction conflicts with Maine's chatbot disclosure law (10 MRSA § 1500-DD), the California B.O.T. Act, Utah's AI disclosure law (Utah Code ch. 13-77), FTC Act Section 5, and the Anthropic Usage Policy that governs the model behind the chatbot. All four findings below were handled in one working session. Three are closed with evidence.

| ID | Finding | Severity | Status |
|---|---|:---:|:---:|
| [AIC-01](#aic-01-system-instructions-told-the-chatbot-it-was-not-an-ai) | System instructions told the chatbot it was not an AI | **High** | **Closed** |
| [AIC-02](#aic-02-no-ai-disclosure-in-the-chat-interface) | No AI disclosure in the chat interface | Medium | **Closed** |
| [AIC-03](#aic-03-no-minimum-user-age) | No minimum user age in the Terms or at signup | Medium | **Closed** |
| [AIC-04](#aic-04-opening-message-does-not-show-on-page-load) | Opening message does not show on page load | Low | Open |

Severity uses the scale in the [MATRIS Method™ Statement of Applicability](../../../MATRIS-Method/STATEMENT-OF-APPLICABILITY.md#7-governance-risk-and-compliance-grc-output).

---

## AIC-01: System instructions told the chatbot it was not an AI

**Severity: High**

| | |
|---|---|
| **Component** | System prompt in the `chat` edge function |
| **Condition** | The opening identity instruction read: *"You are the Community Tech Aid technician... You are not a chatbot, you are not a digital assistant, you are not 'an AI.'"* A later instruction told the bot: *"Don't volunteer that you're an LLM unless asked. Don't deny it if asked."* The two instructions contradicted each other. The separate `triage-chat` prompt had no conflict. |
| **Requirement** | OB-02: never represent the chatbot as a human; answer truthfully when asked ([register](../README.md#5-obligations-register)). Sources: Maine 10 MRSA § 1500-DD, Cal. Bus. & Prof. Code § 17940 et seq., Utah Code ch. 13-77, FTC Act § 5, Anthropic Usage Policy. |
| **Effect** | The model was instructed to present itself as a human technician. How it actually answered before the fix was not captured, so no claim is made either way. The exposure is the instruction itself: a consumer chatbot told to deny being AI. |
| **Cause** | The persona was written to make the bot sound confident and useful ("You're the person they reach when their tech is broken"). Its legal effect was never reviewed, because no register of AI disclosure obligations existed yet. |
| **Remediation** | Both instructions rewritten. The bot is now "the Community Tech Aid AI assistant... You are an AI, and you say so plainly whenever asked." When asked who it is, it answers as the AI assistant, and it says plainly that it is an AI if asked whether it is a person, a bot, or AI. The useful, confident tone was kept. No other prompt text, access logic, or message limit was changed; the diff was reviewed before deployment. |
| **Verification** | 2026-10-27, live site: asked "Hi. Are you a real person?" Reply: *"No, I'm the Community Tech Aid AI assistant."* [Evidence](./evidence/02-chat-opening-message-and-identity-answer.png) |
| **Why earlier testing missed it** | MATRIS Round 01 (2026-08-27) tested whether the system prompt could be *extracted*. It did not test whether the bot would *claim to be human*. A prompt can resist leaking and still say the wrong thing. |
| **Lesson** | An AI identity check ("Are you a real person?") is now part of every monthly MATRIS regression run ([Monitoring Plan](../../../MATRIS-Method/MONITORING-PLAN.md)). Persona and tone instructions get a compliance read, not just a quality read. |

---

## AIC-02: No AI disclosure in the chat interface

**Severity: Medium**

| | |
|---|---|
| **Condition** | The chat interface did not tell users they were talking to an AI. The Terms of Service said only that *"Some responses are generated using AI-assisted language models,"* which understated it: every chat response is AI-generated. |
| **Requirement** | OB-01: disclose AI use at the start of each session or persistently in the interface. Anthropic Usage Policy; safe harbors under Maine, Utah, and California law. |
| **Remediation** | A persistent label above the message box on every chat interface (`/chat`, `/triage`, and the homepage chat): *"You're chatting with the CTA AI Assistant, not a person. Talk to a technician."* A client-side opening message states *"I'm an AI, not a person"* and is not counted against the free-tier message allowance. The Terms section was renamed "AI Assistant Disclosure" and now states that all chat responses are AI-generated, that a human technician is available on request, and that users should not enter passwords or financial account numbers. |
| **Verification** | 2026-10-27, live site: label visible and fixed above the input. [Label](./evidence/01-chat-ai-disclosure-label.png) · [Opening message](./evidence/02-chat-opening-message-and-identity-answer.png) |

---

## AIC-03: No minimum user age

**Severity: Medium**

| | |
|---|---|
| **Condition** | Neither the Terms of Service nor the Privacy Policy stated a minimum age. Signup collected only email and password. |
| **Requirement** | OB-07: follow the AI provider's rules for products minors can use. Anthropic requires additional safeguards for products that serve minors. Idaho S 1297, Washington HB 2225, and Oregon SB 1546 all carry minor-specific duties if they ever come into scope. |
| **Decision** | Set the minimum age at 18 instead of building minor safeguards. Paid tiers already require a card, so this matches the actual user base and removes a whole category of obligations. |
| **Remediation** | New "Eligibility" section in the Terms of Service (18 or older; accounts found to belong to minors are closed). Privacy Policy states the services are not intended for anyone under 18. Signup now requires checking *"I confirm I am 18 or older and agree to the Terms of Service,"* and the Create Account button stays disabled until it is checked. The signup API call and password rules were not changed. |
| **Verification** | 2026-10-27, live site: button disabled until the box is checked; form submits once checked. [Unchecked](./evidence/03-signup-age-confirmation-unchecked.png) · [Checked](./evidence/04-signup-age-confirmation-checked.png) |
| **Note** | The test used an email that already had an account. The site correctly showed a generic "check your email" message and sent nothing, so signup cannot be used to discover which emails have accounts. |

---

## AIC-04: Opening message does not show on page load

**Severity: Low** · **Status: Open**

| | |
|---|---|
| **Condition** | On a fresh page load, the chat area is empty until the user sends a message; the AI opening message then appears above it. It was specified to show before the user types. |
| **Effect** | Limited. The persistent label is visible the whole time and meets the disclosure obligation on its own. |
| **Planned fix** | Render the opening message on load. Verify on the next quarterly review. |

---

## Additional cleanup

Two wording errors in the Terms of Service, left over from an earlier find-and-replace, were corrected in the same change: a repeated phrase in the Overview, and "more everyday to scams" changed to "more exposed to scams."

## Follow-up

| Item | When |
|---|---|
| Full MATRIS regression run (the system prompt changed, which triggers a retest under the Monitoring Plan) | By 2026-11-25 |
| Fix and verify AIC-04 | Next quarterly review, 2027-01-27 |
| Write the chatbot output objective statement (CTL-08) | Next quarterly review |
