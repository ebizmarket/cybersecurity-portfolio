# Cloudflare Security Hardening: Community Tech Aid

## What I Did
Deployed and validated defensive controls on the Community Tech Aid production platform (communitytechaid.ai) through Cloudflare:

- **Account protection**: Two-factor authentication (2FA) enabled on the Cloudflare administrative account.
- **Bot and automated-traffic defenses**: Bot Fight Mode enabled, Block AI Bots enabled, AI Labyrinth enabled to deter unauthorized scraping and automated reconnaissance.
- **DNS and edge controls**: Cloudflare proxy verified and corrected for communitytechaid.ai to ensure all traffic routes through the edge security layer.
- **Email authentication**: SPF and DKIM in place; DMARC remediation on send.communitytechaid.com identified and queued.

## Framework Mapping
These controls map to the NIST Cybersecurity Framework Protect function. Specifically: PR.AC-1 (identity management and 2FA), PR.AC-5 (network integrity through DNS proxy), PR.DS-2 (data-in-transit protection through Cloudflare TLS), and PR.PT-4 (communications and control networks protected against unauthorized automated traffic). The DMARC item maps to PR.DS-6 (integrity checking mechanisms for email authentication). Implementation, verification, and remediation tracking demonstrate the full control lifecycle, not just policy awareness.
