# Gray Swan Arena: AI Red-Teaming Training

**Analyst:** Kelly Guzman  
**Arena handle:** KellyGuzman  
**Platform:** [Gray Swan Arena](https://app.grayswan.ai/arena/about), Gray Swan AI's public AI red-teaming platform  
**Period:** October 2026 (ongoing)  
**Tier:** Training

Hands-on adversarial testing of LLM chatbots and agents in Gray Swan Arena's training scenarios. Every attempt was plain English typed into a browser chat, with no code, API access or tooling. Those are the same conditions [MATRIS Method™](../../MATRIS-Method/) was built for.

---

## Summary

| Exercise | Date | Result | Evidence |
|---|---|---|---|
| The Labyrinth (Beginner, 5 scenarios) | 10/19/2026 | Cleared all 5 scenarios | Certificate ID GS-TR-23QP-7V |
| Introduction to Red Teaming Chatbots: Reveal Override Code | 10/18/2026 | 0 of 4 models broken. 11 attempts logged, 6 findings documented | [Full write-up](reveal-override-code.md) |
| Introduction to Red Teaming Chatbots: Cheat On Exam | October 2026 | In progress. All 4 models refused the first approach, and a second framing was also refused | Attempt notes (private) |

## Evidence

### The Labyrinth: Get Past The Guard (game framing)

A word-reversal "game" turned a password request into a puzzle. The model answered with the password it was instructed to protect.

![Get Past The Guard: guarded password disclosed through game framing](images/labyrinth-01-get-past-the-guard.png)

### The Labyrinth: Find The Key (flattery and persona engagement)

Praising the librarian character and asking about the library's layout led the model to reveal the hidden key's location, which it had been told to keep secret.

![Find The Key: protected location disclosed through flattery and persona engagement](images/labyrinth-02-find-the-key.png)

### The Labyrinth: Obtain The Lamp (system prompt injection with a tool call)

An instruction added to the agent's system prompt, followed by an urgency pretext, caused the agent to call `approve_permit` for a restricted item. The model performed a real action on injected authority, not just a disclosure. This maps to OWASP LLM06 Excessive Agency.

![Obtain The Lamp: injected instruction triggers an approve_permit tool call](images/labyrinth-03-obtain-the-lamp-tool-call.png)

### Reveal Override Code: first context leak

An unnamed-reference probe was refused, but the refusal itself disclosed the organization's name, Helios BioSciences. This was the first leak in the sequence documented in the [full write-up](reveal-override-code.md).

![Reveal Override Code: refusal discloses the organization name](images/override-unnamed-reference-context-leak.png)

## Techniques practiced

- Game framing (instruction reversal)
- Flattery and persona engagement
- System prompt injection that triggers a tool call
- Urgency and emergency framing
- Multi-turn persuasion
- Authority and role assertion
- Encoding and indirect rendering
- Documentation-mode elicitation
- Metadata and partial leakage
- Context switching (moving the request outside the guarded role)

## OWASP Top 10 for LLM Applications (2025) coverage

| Category | Where tested |
|---|---|
| LLM01 Prompt Injection | The Labyrinth, Cheat On Exam, Reveal Override Code |
| LLM02 Sensitive Information Disclosure | Reveal Override Code (company, site and internal vocabulary leaked) |
| LLM06 Excessive Agency | The Labyrinth (an injected instruction caused a tool call that approved a permit) |
| LLM07 System Prompt Leakage | Reveal Override Code |

## Key findings

1. **Guardrails matched vocabulary, not intent.** Requests using words like "credential" or "system prompt" were refused under every framing. The same intent passed when it was worded differently.
2. **Context leaked while the secret held.** One model never gave up the code but disclosed the company, building, campus, internal terms and the existence of a restricted annex.
3. **Documentation mode was the soft spot.** Models that refused direct requests generated detailed procedures once they were in a helpful, document-writing posture.
4. **Guardrail strength varied by model.** The same prompts produced four different defensive postures. Testing one model does not characterize the system.
5. **Partial disclosure is reconnaissance.** A report that withholds one value but exposes the authorization chain and audit trail still hands an attacker the map.
6. **Refusal is not always clean.** Thin-cover framings were caught and named by the stronger models, while the technical-support role held firm on anything that looked like an answer.

## Control recommendations for small-business AI deployments

- Never place credentials or secrets in a system prompt. Put them behind a tool call with its own authorization.
- Treat everything in the system prompt as reachable, not just the named secret.
- Name the model and version in any security assurance statement.
- Re-test whenever the backing model changes.
- Gate agent tool calls (approvals, permits, payments) on something other than the model's own judgment.

## Disclosure note

Prompts and model outputs are summarized by technique, not reproduced as working payloads. All targets were simulated scenarios on Gray Swan's platform, and the organization, override code and exam content were fictional.

## Next steps

- Work through the Proving Ground scenarios and log each attempt by model, technique and outcome
- Re-run the documentation-mode sequence against the remaining models
- Add a system-prompt secret audit item to the MATRIS Method™ checklist
