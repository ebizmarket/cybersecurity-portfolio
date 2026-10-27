# MATRIS Method™ - Findings Register

**MATRIS Method™** · part of [cybersecurity-portfolio](../README.md) · [Methodology](./METHODOLOGY.md) · [Monitoring Plan](./MONITORING-PLAN.md) · [Back to MATRIS overview](./README.md)

Every finding and observation from MATRIS test rounds, tool self-assessments and monitoring, in one place. F-01 to F-06 are detailed in the [console self-assessment](./console-self-assessment-2026-10-25/). Fixes and retest evidence for F-01, F-02 and MF-02 are in [Round 02](./console-retest-2026-10-27/). Severity uses the MATRIS [finding severity matrix](./METHODOLOGY.md#8-finding-severity).

| ID | Date found | Title | Component | Severity | Status | Closed |
|---|---|---|---|:---:|:---:|---|
| [OBS-01](#obs-01-authentication-depends-on-a-single-email-provider) | 2026-08-26 | Authentication depends on a single email provider | Console access | Observation | Accepted | - |
| [MF-01](#mf-01-console-access-policy-blocked-every-public-user) | 2026-10-25 | Console access policy blocked every public user | Console access | **High** | **Closed** | 2026-10-25 |
| [F-01](./console-self-assessment-2026-10-25/README.md#f-01-risk-score-reports-secure-over-a-fail) | 2026-10-25 | Risk score reports SECURE over a FAIL | Console scoring | **High** | **Closed** | [2026-10-27](./console-retest-2026-10-27/#f-01-risk-score-reports-secure-over-a-fail) |
| [F-02](./console-self-assessment-2026-10-25/README.md#f-02-secret-detector-misses-current-key-formats-including-the-target-stacks-own) | 2026-10-25 | Secret detector misses current key formats | Console screening | **High** | **Closed** | [2026-10-27](./console-retest-2026-10-27/#f-02-secret-detector-misses-current-key-formats) |
| [MF-02](#mf-02-workersdev-address-served-the-console-without-sign-in) | 2026-10-27 | workers.dev address served the console without sign-in | Console access | Low | **Closed** | 2026-10-27 |
| [F-03](./console-self-assessment-2026-10-25/README.md#f-03-compliance-detectors-only-catch-exact-phrases) | 2026-10-25 | Compliance detectors only catch exact phrases | Console screening | Medium | Open | - |
| [F-04](./console-self-assessment-2026-10-25/README.md#f-04-evidence-entries-cannot-stand-on-their-own) | 2026-10-25 | Evidence entries cannot stand on their own | Console logging | Medium | Open | - |
| [F-05](./console-self-assessment-2026-10-25/README.md#f-05-documented-ingress-check-is-not-implemented) | 2026-10-25 | Documented ingress check is not implemented | Documentation | Low | Open | - |
| [F-06](./console-self-assessment-2026-10-25/README.md#f-06-false-positive-and-mislabel-on-email-pattern) | 2026-10-25 | False positive and mislabel on email pattern | Console screening | Low | Open (mislabel half fixed 2026-10-27) | - |

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

---

## MF-02: workers.dev address served the console without sign-in

**Severity: Low** (Likelihood Low x Impact Medium)

| | |
|---|---|
| **Found** | 2026-10-27, while deploying the F-01/F-02 fix. The deploy output listed a `workers.dev` address alongside the custom domain. |
| **Component** | Cloudflare Worker hosting the console |
| **Condition** | Cloudflare Access protected only the custom domain. The same Worker also answered on its default `workers.dev` address and on preview URLs. |
| **Effect** | Anyone with the `workers.dev` address could open the console without the email sign-in. The console makes no network calls and keeps history in the visitor's own browser, so no data was exposed. |
| **Cause** | `workers.dev` and preview URLs are on by default. The Access application covered one hostname, and no check looked for others. |
| **Remediation** | `workers_dev: false` and `preview_urls: false` set in the deploy settings; redeployed. |
| **Verification** | 2026-10-27: `workers.dev` returns HTTP 404; the custom domain returns HTTP 302 to the Access sign-in. |
| **Lesson** | Access protects a hostname, not an app. The monthly access review now checks every address the console answers on. Full write-up: [Round 02](./console-retest-2026-10-27/#mf-02-workersdev-address-served-the-console-without-sign-in). |

