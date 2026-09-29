# SENTIALA THREAT INTELLIGENCE REPORT

**Target:** `http://malicious.test/download`  
**Target type:** url  
**Generated:** 2026-09-28T04:49:21+00:00  
**Threat level:** 🟠 **HIGH RISK**  
**Risk score:** **68/100**  
**Confidence:** **97%**

**Public intelligence status:** 2 relevant intelligence finding(s) found

## Why Sentiala assesses this risk

Sentiala assessed 'http://malicious.test/download' as HIGH RISK (risk score 68/100) by correlating the following evidence: • Host listed on URLhaus malware feed (+45 points, VERIFIED FACT, source: URLhaus (abuse.ch)). • Domain registered only 13 days ago (+15 points, VERIFIED FACT, source: RDAP (registry data)). • No transport encryption (not HTTPS) (+8 points, OBSERVATION, source: Sentiala local deterministic rules). Of these, 2 finding(s) are verified facts confirmed by external sources; the remainder are deterministic observations from URL structure and infrastructure analysis. The high verdict reflects the combination of multiple independent indicators rather than any single signal. This explanation is a rule-based correlation of the evidence above, produced by Sentiala's local deterministic correlator.

## Evidence

### VERIFIED FACT

- **Host listed on URLhaus malware feed** (+45 pts) — The host 'malicious.test' is listed in the URLhaus malware intelligence feed. Reference: https://urlhaus.abuse.ch/host/malicious.test/ _(source: URLhaus (abuse.ch), Tier 2 (trusted), 2026-09-28T04:49:21+00:00)_
- **Domain registered only 13 days ago** (+15 pts) — 'malicious.test' was registered on 2026-09-14. Phishing infrastructure is frequently brand new; legitimate established sites are rarely this young. _(source: RDAP (registry data), Tier 1 (highest confidence), 2026-09-28T04:49:21+00:00)_

### OBSERVATION

- **No transport encryption (not HTTPS)** (+8 pts) — Credentials or data submitted to this target would travel in cleartext. _(source: Sentiala local deterministic rules, Tier 1 (highest confidence), )_

### AI INFERENCE

_None for this investigation._

### UNVERIFIED CLAIM

_None for this investigation._

## Score contributions

| Indicator | Points | Evidence class | Source |
|---|---|---|---|
| Host listed on URLhaus malware feed | 45 | VERIFIED FACT | URLhaus (abuse.ch) |
| Domain registered only 13 days ago | 15 | VERIFIED FACT | RDAP (registry data) |
| No transport encryption (not HTTPS) | 8 | OBSERVATION | Sentiala local deterministic rules |

## Possible false positives

- No mitigating factors observed for this target.

## Live intelligence status

- URLhaus (abuse.ch): available (host is listed)
- RDAP (registry data): available
- Cloudflare DNS-over-HTTPS: available (resolves (1 A record(s)))

## Recommended action

**Strong evidence of malicious activity. Do not enter credentials or download files; close the site and reach the service through its official domain instead.**

## Sources

- Sentiala local deterministic rules — Tier 1 (highest confidence) (local://deterministic-url-analyzer)
- URLhaus (abuse.ch) — Tier 2 (trusted) (https://urlhaus.abuse.ch/)
- RDAP (registry data) — Tier 1 (highest confidence) (https://rdap.org/)

---
_Sentiala provides evidence-based security assistance. It does not guarantee detection of every threat, and a SAFE verdict means 'no significant evidence found', not 'verified safe'._