# CTA NIST SP 800-53 Rev 5 Compliance Package

GRC and Compliance · part of cybersecurity-portfolio

A complete, four-document control package for a live production system, assessed
against the NIST SP 800-53 Revision 5 LOW baseline. The system is Community Tech
Aid (communitytechaid.ai), a consumer AI tech-support web application operated by
eBiz Market, LLC. It is a real system with real users, not a training scenario.

## Contents

| Entry | Title | Format | Status |
|---|---|---|---|
| 01 | System Security Plan (control implementation statements) | .md / .pdf | Complete |
| 02 | Security Policy Manual (18 control-family policies) | .md / .pdf | Complete |
| 03 | Security Assessment Report and POA&M | .md / .pdf | Complete |
| 04 | Security Posture Summary (plain language, client facing) | .md / .pdf | Complete |

Read them in that order. Each one depends on the one before it.

## What each document does

**01 - System Security Plan.** Defines the authorization boundary in three layers
(system-owned, inherited, external), the data types and PII, the data flows, and a
customer responsibility matrix assigning every control to Provider, Shared, or
Customer. Then an implementation statement, evidence list, and status for each of
136 controls. Includes a findings and remediation log and a stated gap list.

**02 - Security Policy Manual.** One policy per applicable control family, 18 in
total, satisfying the family "-1" (Policy and Procedures) control for each. Purpose
and scope, roles, policy statements, procedures, inherited responsibilities, known
limitations, and a review cadence.

**03 - Security Assessment Report.** Assesses the plan against NIST SP 800-53A Rev 5
methods (Examine, Interview, Test). Per-control determinations, 20 findings with
condition, effect, cause, and recommendation, and a 20-item POA&M with owners and
target dates. Records three controls where the assessor's determination is less
favorable than the plan claims.

**04 - Security Posture Summary.** The same results written for a non-technical
reader. No control identifiers, no code paths. Intended for a prospective partner,
customer, or buyer.

## Assessment results

| Result | Count |
|---|--:|
| Satisfied | 42 |
| Satisfied (Inherited) | 25 |
| Other Than Satisfied | 51 |
| Not Applicable | 18 |
| **Total assessed** | **136** |

Satisfied results cluster in access control, identification and authentication, and
the policy families. Other Than Satisfied results cluster in contingency planning,
incident response, continuous monitoring, and configuration management. That is the
signature of a system built carefully and governed informally, and the POA&M in
document 03 is the plan to close it.

## Notes on scope and honesty

This is a **self-assessment**. The same person built the system, wrote the plan, and
performed the assessment. Independence is not required at the LOW impact level, but
the absence of it is part of the result and is stated in the report rather than
implied away.

Twenty-five controls are inherited from Lovable Cloud, Cloudflare, and Stripe with
no provider attestations on file. The report names this as its single largest
evidentiary weakness rather than presenting inherited controls as verified.

Seven security weaknesses were self-identified and remediated during and immediately
before the assessment period, including a broken access control condition in the paid
access gate and a forgeable audit log. They are documented in document 01 rather than
quietly patched.

## Why this package exists

Most GRC portfolio work assesses a fictional company against a framework. This
assesses a system that is deployed, takes payments, and holds user data, where a
wrong control decision has a consequence. The gaps are real gaps and they are named.

---

*Prepared 2026-07-27 · eBiz Market, LLC (Idaho) · communitytechaid.ai*
