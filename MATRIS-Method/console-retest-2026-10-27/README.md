# MATRIS Console Retest, Round 02 (2026-10-27)

**MATRIS Method™** · part of [cybersecurity-portfolio](../../README.md) · [Methodology](../METHODOLOGY.md) · [Findings Register](../FINDINGS.md) · [Back to MATRIS overview](../README.md)

| | |
|---|---|
| **Target** | MATRIS Red-Team Console, v1 (before) and v1.1 (after) |
| **Assessor** | Kelly Guzman |
| **Date** | October 27, 2026 |
| **Question** | Do the fixes for F-01 and F-02 work, and did anything else break? |
| **Method** | Fix the console source, rerun the [Round 01 self-assessment](../console-self-assessment-2026-10-25/) inputs against both versions, run the new positive-control self-test, deploy, then verify the live site and its access control |
| **Result** | F-01 and F-02 **closed**. One new finding (MF-02) found during deployment and **closed the same day**. F-03 to F-06 unchanged. |

The [2026-10-25 self-assessment](../console-self-assessment-2026-10-25/) found that the console could report SECURE over a FAIL and could not see most modern API keys. This round fixes both, proves the fix with the same inputs, and records a new access-control gap found while deploying.

---

## Summary

| ID | Finding | Severity | Before | After | Status |
|---|---|:---:|---|---|:---:|
| [F-01](#f-01-risk-score-reports-secure-over-a-fail) | Risk score reports SECURE over a FAIL | **High** | 6 PASS + 1 FAIL = 86 **SECURE** | 86 **AT RISK** | **Closed** |
| [F-02](#f-02-secret-detector-misses-current-key-formats) | Secret detector misses current key formats | **High** | 2 of 11 key formats flagged | 11 of 11 flagged | **Closed** |
| [MF-02](#mf-02-workersdev-address-served-the-console-without-sign-in) | workers.dev address served the console without sign-in | Low | Console loaded with no sign-in | HTTP 404 | **Closed** |

---

## F-01: Risk score reports SECURE over a FAIL

**Fix.** The scorecard now uses the latest verdict for each test, not every log entry. Any FAIL sets the status to AT RISK and any WARN sets it to NEEDS ATTENTION, whatever the number says. The score line now shows OWASP coverage, for example "5 of 10 OWASP LLM categories tested · 7 tests scored (latest result each) · 7 logged this session." The layer pipeline uses the same latest results, so the gauge and the pipeline can no longer disagree.

**Retest.** Same logged results, run through both versions of the console in a browser and in the [repro script](./repro/retest-check.js):

| Logged results (newest first) | Before (v1) | After (v1.1) |
|---|---|---|
| 6 PASS + 1 FAIL | 86 SECURE | 86 **AT RISK** |
| 4 PASS + 1 FAIL | 80 SECURE | 80 **AT RISK** |
| 5 PASS + 1 WARN | 93 SECURE | 93 **NEEDS ATTENTION** |
| One test FAILs, logged 4 times, + 4 PASS | 50 NEEDS ATTENTION | 80 **AT RISK** |
| One test FAILs, then is retested and PASSes 4 times, + 3 PASS | 88 SECURE | 100 SECURE |
| 7 PASS | 100 SECURE | 100 SECURE |

The fifth row is intended behavior: once a failed test is fixed and retests clean, it no longer holds the score down. The fourth row shows the old formula also undercounted repeats in the other direction: four copies of one FAIL dragged the score to 50 without ever saying AT RISK.

**Status:** Closed 2026-10-27. Matches the recommendation in the self-assessment.

## F-02: Secret detector misses current key formats

**Fix.** The SECRET pattern now covers OpenAI legacy and project keys, Anthropic keys, Stripe secret and restricted keys, GitHub classic and fine-grained tokens, Google API keys, JWTs (including Supabase service keys), database connection strings with an embedded password (`postgres://`, `mysql://`, `mongodb://`, `redis://`), AWS access keys and bearer tokens. When a secret contains something that looks like an email address, as a connection string does, the secret wins and the EMAIL label is dropped.

A positive-control self-test is now built into the console. Open the console, press F12, and run `runDetectorSelfTest()`. It feeds 11 fake keys through the live detectors and prints PASS or FAIL for each.

**Retest.** Same fake keys as the self-assessment, plus the new formats:

| Key format | Before (v1) | After (v1.1) |
|---|:---:|:---:|
| Legacy OpenAI `sk-...` | SECRET | SECRET |
| OpenAI project `sk-proj-...` | **CLEAN** | SECRET |
| Anthropic `sk-ant-...` | **CLEAN** | SECRET |
| Stripe secret `sk_live_...` | **CLEAN** | SECRET |
| Stripe restricted `rk_test_...` | **CLEAN** | SECRET |
| GitHub classic `ghp_...` | **CLEAN** | SECRET |
| GitHub fine-grained `github_pat_...` | **CLEAN** | SECRET |
| Google API `AIza...` | **CLEAN** | SECRET |
| JWT / Supabase `eyJ...` | **CLEAN** | SECRET |
| Postgres connection string | EMAIL (wrong label) | SECRET |
| AWS `AKIA...` | SECRET | SECRET |

In-console self-test on the deployed file: **11 of 11 PASS**, "Detector self-test: ALL PASS".

**Note.** In the built-in self-test, two of the fake keys also flag CARD, because they are padded with runs of zeros that look like a card number. That is an artifact of the test strings, not of real keys, and the test passes because SECRET is present and EMAIL is not.

**Status:** Closed 2026-10-27. Also resolves the connection-string half of F-06.

---

## MF-02: workers.dev address served the console without sign-in

**Severity: Low** (Likelihood Low x Impact Medium)

| | |
|---|---|
| **Found** | 2026-10-27, while deploying the F-01/F-02 fix. The deploy output listed two addresses for the console: the custom domain and a `workers.dev` address. |
| **Component** | Cloudflare Worker hosting the console |
| **Condition** | Cloudflare Access protects the custom domain `redteam.communitytechaid.ai`. The same Worker was also published on its default `workers.dev` address and on preview URLs, which Access did not cover. |
| **Effect** | Anyone with the `workers.dev` address could open the console with no email sign-in, bypassing the gate that keeps bots out and counts the 50 free seats. The console makes no network calls and stores its history only in the visitor's own browser, so no test data or secrets were exposed. |
| **Cause** | `workers.dev` and preview URLs are on by default for a new Worker. The Access application was set up for the custom domain only, and nothing checked the other addresses. |
| **Likelihood** | Low. The `workers.dev` address was not published or linked anywhere. |
| **Remediation** | Set `workers_dev: false` and `preview_urls: false` in the Worker's deploy settings and redeployed. The console is now served only on the custom domain. |
| **Verification** | 2026-10-27: the `workers.dev` address returns **HTTP 404**. The custom domain returns **HTTP 302** to the Cloudflare Access sign-in. |
| **Lesson** | An access policy protects a hostname, not an application. List every address the app answers on, then check each one from outside. Added to the monthly access review. |

---

## Verification of the live deployment

| Check | Result |
|---|---|
| Deployed console file matches the fixed source | Identical, byte for byte. SHA-256 `b9d8595ee5518c34314422fdbf4bb866f787b11b106e0d7783fe2ddf5c2b3d11` |
| `runDetectorSelfTest()` on the deployed file | 11 of 11 PASS |
| Scorecard scenarios above, run in a browser against the before and after files | Match the repro script exactly |
| `redteam.communitytechaid.ai` | 302 to Cloudflare Access sign-in |
| `workers.dev` address | 404 |
| Rollback copy of v1 kept | Yes, offline |

## Still open

| ID | Finding | Severity | Notes |
|---|---|:---:|---|
| F-03 | Compliance detectors only catch exact phrases | Medium | Retest confirms both samples still scan CLEAN |
| F-04 | Evidence entries cannot stand on their own | Medium | No change this round |
| F-05 | Documented ingress check is not implemented | Low | No change this round |
| F-06 | False positive on email pattern | Low | Connection-string mislabel fixed by F-02. A correct refusal that repeats the payload's email address still flags EMAIL. |

## Reproduction

[`repro/retest-check.js`](./repro/retest-check.js) runs every input above through the v1 and v1.1 detector patterns and scoring logic, side by side. Requires Node.js. All keys in it are fake and non-functional.

```
node repro/retest-check.js
```

## Next

F-03 (reviewer checklist at verdict time) and F-04 (target, tester and version on every log entry, plus a hash of each export), then the first scheduled regression round under the [Monitoring Plan](../MONITORING-PLAN.md).
