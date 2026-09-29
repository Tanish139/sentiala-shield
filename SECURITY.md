# Security Policy — Sentiala Shield

## Scope: defensive security only

Sentiala Shield is a **defensive** cybersecurity product. The following
will never be implemented, in this repository or any Sentiala component:

- credential theft, password extraction, keylogging, cookie theft
- hidden surveillance, covert persistence, stealth monitoring of other people
- unauthorized remote access or authentication bypass
- malware, ransomware, or any offensive tooling
- secret collection of private communications
- exploitation of systems without authorization
- bypassing access controls, robots.txt, ToS, or licensing of any source

All analysis operates on public information and on the user's own
activity, with user knowledge. Monitoring of others is out of scope.

## What the code does today

- Reads a URL/domain/IP/hash that the user (or their browser, with
  consent, in a later phase) submits for analysis.
- Runs deterministic, local analysis. Never fetches the target URL.
- Sends **only hostnames** to public intelligence services
  (URLhaus, RDAP, Cloudflare DoH) when online intelligence is enabled.
- Stores history and intelligence cache locally under the data directory.
- Never logs or transmits credentials, cookies, tokens, or private keys.

## Tool permission system

`python -m sentiala_core.cli permissions` prints the current
permissions. Read-only public lookups are allowed by default; anything
touching local files requires explicit user approval; credential access
and remote control are denied at the architecture level.

## Reporting a vulnerability

Please open a private security advisory on this repository
(GitHub → Security → Advisories) or contact the maintainers directly.
Do not open public issues for exploitable flaws.

We commit to:

- acknowledging reports within 72 hours,
- no legal action against good-faith research that respects user privacy,
- credit in the changelog (opt-in).

## Secret hygiene

- Real API keys must never be committed. `.env` is gitignored.
- `.env.example` documents every planned variable with empty values.
- The browser extension will never embed private server API keys; all
  intelligence flows through the local core.
