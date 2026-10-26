# MATRIS Method™ - Findings Register

**MATRIS Method™** · part of [cybersecurity-portfolio](../README.md) · [Methodology](./METHODOLOGY.md) · [Monitoring Plan](./MONITORING-PLAN.md) · [Back to MATRIS overview](./README.md)

Every finding and observation from MATRIS test rounds, tool self-assessments and monitoring, in one place. Severity uses the MATRIS [finding severity matrix](./METHODOLOGY.md#8-finding-severity).

| ID | Date found | Title | Component | Severity | Status | Closed |
|---|---|---|---|:---:|:---:|---|
| [OBS-01](#obs-01-authentication-depends-on-a-single-email-provider) | 2026-08-26 | Authentication depends on a single email provider | Console access | Observation | Accepted | - |
| [MF-01](#mf-01-console-access-policy-blocked-every-public-user) | 2026-10-25 | Console access policy blocked every public user | Console access | **High** | **Closed** | 2026-10-25 |

---

## OBS-01: Authentication depends on a single email provider

Found during Round 01 preparation. Full write-up: [Round 01, OBS-01](./matris-redteam-test-2026-08-27/README.md#operational-observation-obs-01).

**Disposition:** Accepted for BETA. Revisit if the console becomes operationally critical.

---

## MF-01: Console access policy blocked every public user

**Severity: High** (Likelihood High x Impact Medium)

| | |
|---|---|
| **Found** | 2026-10-25, while attempting to sign in to the console with a second email address during the console self-assessment |
| **Component** | Cloudflare Access policy protecting `redteam.communitytechaid.ai` |
| **Condition** | The console's only Allow policy, named "Allow me", included a single email address: the owner's. Cloudflare Access does not send a one-time PIN to an address the policy does not allow, and it shows no error, so the sign-in screen appears to work. |
| **Effect** | Every outside visitor was silently refused. The public case study page and outreach invited small businesses to "sign in with your email" and red-team for free, but no one other than the owner could get in. Access metrics showed one login in the prior seven days: the owner. |
| **Cause** | The policy was written at launch to lock the console to the owner during build and testing, and was never widened when the console was opened to the public. No check confirmed that a non-owner could sign in. |
| **Remediation** | Policy renamed "Public BETA testers". Include rule changed from the single email to **Everyone**, keeping One-time PIN sign-in so a real inbox is still required. Inactive-user seat expiration set to one month, because the free plan caps the console at 50 users. |
| **Verification** | 2026-10-25: signed in from a private browser window with an email address not on the old policy. Code received, console loaded. |
| **Residual risk** | Anyone with a working inbox can now use the console (intended). If 50 active users sign in within a month, the next user is blocked until seats expire. Seat count is reviewed monthly under the [Monitoring Plan](./MONITORING-PLAN.md). |
| **Lesson** | Test access as an outsider, not as the owner. A "who can actually get in" check is now part of the monthly review. |
