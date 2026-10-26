# Security Posture Summary

## Community Tech Aid

**A service of eBiz Market, LLC | communitytechaid.ai**

*Tech help that doesn't make you feel stupid.*

**Prepared:** July 27, 2026
**Prepared for:** prospective partners, buyers, and anyone deciding whether to trust this service with their data
**Covers:** the Community Tech Aid web application at communitytechaid.ai

---

## Why this document exists

Most small companies say "we take security seriously" and leave it there. That sentence costs nothing and proves nothing.

So instead, Community Tech Aid was measured against the U.S. government's published security standard for information systems, and this is the plain-language result. It says what is protected well, what is not finished, and when the unfinished parts are due. Nothing here is hidden behind jargon, and the parts that look bad are still in here.

That is the point. A security summary you can only trust if you don't read it closely is not worth writing.

---

## What Community Tech Aid actually is

Community Tech Aid is a website where a person with a computer problem can get real help. Scams, slow machines, popups, WiFi, WordPress, TVs and soundbars. An AI assistant does the troubleshooting, and if that isn't enough, a real human takes over by email.

It is run by one person: the owner of eBiz Market, LLC, an Idaho company. There are no employees. That fact shapes everything in this document, and it is stated up front rather than disguised with corporate language.

---

## What information the service holds

| We hold | We do not hold |
|---|---|
| Your email address, used as your account name | Credit card numbers |
| The chat conversations you have with the assistant | Social Security numbers |
| What you send through the contact form | Bank account details |
| Basic visit and sign-in records, including your IP address | Medical or health records |
| Whether your account is free or paid, and when it expires | Anything about children, knowingly |

Payments are handled entirely by Stripe on Stripe's own pages. Card details never touch this service. The only thing that comes back is whether you paid and when your access ends.

---

## How the service was measured

The measuring stick is **NIST SP 800-53 Revision 5**, the security control catalog the U.S. federal government uses for its own systems. It was applied at the **LOW** level, which is the correct level for a small consumer service that holds no government, financial, or medical data.

**136 individual security requirements** were checked, one at a time. For each one the question was the same: is this actually in place, does it actually work, and can it be proven?

Three documents came out of that work, and all three are published:

1. A **System Security Plan** describing how every requirement is met and where it isn't.
2. A **Security Policy Manual** stating the standing rules the business commits to.
3. A **Security Assessment Report** grading the first two and listing every open item with a due date.

This document is the readable summary of all three.

---

## The results

| Result | Count | What it means |
|---|--:|---|
| **Met** | 42 | Built, working, and verified |
| **Met by our providers** | 25 | Handled by Cloudflare, Stripe, and the hosting platform, and relied upon |
| **Doesn't apply** | 18 | Requirements about employees, offices, and hardware that don't exist here |
| **Open** | 51 | Not finished. Every one has a plan and a date |

### Reading that honestly

51 open items out of 136 sounds alarming. Here is what is actually behind that number.

**The parts that protect your data are done.** Every user can reach only their own records, enforced in the database itself rather than only in the website. The AI assistant can only be reached by a signed-in account. Payment status is verified on the server, never taken on the browser's word. Sign-in records cannot be faked by a visitor. Those were all tested, not just claimed.

**The parts that are open are mostly paperwork.** They cluster in four areas: a written disaster recovery plan, a written incident response plan, a verified independent backup, and a formal monitoring routine. These are real gaps and they are treated as real. But none of them is a hole an attacker walks through. They are the difference between a system that is built carefully and a system that is also *governed* carefully, and the second one is what the next several months are for.

---

## What is genuinely strong

**Security problems get found and fixed, with a paper trail.** Seven real weaknesses were discovered and closed in the weeks before this summary, several of them the same day they were found. One of them would have let someone unlock paid access by editing a value in their own browser. Another would have let a visitor write fake entries into the sign-in log. Both are closed, and both are written up in public rather than quietly patched.

A company that can show you the bugs it found in itself is telling you more than a company with a clean record and no evidence.

**Protection sits at the deepest layer, not the surface.** The rules about who can see which data are enforced by the database, not by the website. If the website were compromised tomorrow, the data would still not hand itself over. This is the harder way to build it and it is the right way.

**The documentation admits what it doesn't do.** The security plan uses present tense for what exists and names what doesn't. There is no aspirational language, no "we are committed to" standing in for "we have."

---

## What is not finished, and when it will be

Every open item has an owner and a date. These are the ones that matter most.

| What | Why it matters | Due |
|---|---|---|
| An independent backup, plus one real test restore | Backups currently come from the hosting platform and have never been restored. An untested backup is a hope, not a safeguard. This is the single most valuable item on this list. | Aug 31, 2026 |
| A written incident response plan | If something goes wrong, response is currently a matter of judgment in the moment. It needs to be a written procedure, including who gets told and how fast. | Sep 15, 2026 |
| A written disaster recovery plan, and a test of it | There is no stated answer to how long recovery takes or how much data could be lost. That answer needs to exist before it is needed. | Sep 30, 2026 |
| A defined monitoring routine | Alerts exist for specific problems. A defined list of what gets watched, how often, and what triggers action does not yet. | Sep 30, 2026 |
| Provider security reports on file | 25 requirements are handled by outside providers, and their reports have not been collected. Collecting them turns 25 assumptions into 25 pieces of evidence. | Oct 15, 2026 |

There are fifteen more items below these, all documented with dates in the full assessment report.

---

## What you should know before you rely on this

Three limits, stated plainly, because a summary that hides them is worse than no summary.

**This was a self-assessment.** The person who built the system also graded it. That is permitted at this security level and it is common for a company this size, but it is not the same as an outside audit. Nothing here has been checked by an independent party.

**Some things cannot be verified from the inside.** The service runs on a managed platform where the owner does not hold the deepest administrative keys. Several protections are therefore taken on the provider's word rather than tested directly. That is disclosed here rather than presented as verified.

**No outside security testing has been done.** There has been no penetration test and no external vulnerability scan. The testing performed was code review, configuration review, dependency scanning, and hands-on checks of specific access paths.

If any of that matters to your decision, the right response is to ask for an independent assessment rather than to take this one at a higher value than it claims.

---

## The bottom line

Community Tech Aid is a small service, built by one technician, that holds a small amount of low-risk personal information and no financial or medical data. It was measured against a federal security standard rather than a marketing checklist, and the measurement is published in full, including the parts that came back short.

The technical protections around user data are in place and were tested. The written procedures that would carry the service through a bad day are being built now, on a schedule, in public.

That is the honest position. It is not a perfect score, and a perfect score from a one-person company would be the less believable answer.

---

## Documents behind this summary

All three are published and available in full:

- **System Security Plan** - how each of the 136 requirements is handled
- **Security Policy Manual** - the standing rules, covering all 18 policy areas
- **Security Assessment Report** - the grading, the 20 findings, and the dated plan to close them

## Contact

**Community Tech Aid**, a service of eBiz Market, LLC (Idaho)
communitytechaid.ai | support@communitytechaid.ai

*This summary reflects the state of the service as of July 27, 2026. It is reviewed at least annually and after any significant change.*
