# Contributing to Sentiala Shield

Thank you for helping build a defensive, privacy-first security platform.

## Ground rules

1. **Defensive only.** Contributions that add offensive capability,
   covert monitoring, or data collection beyond what is documented will
   be rejected. See [SECURITY.md](SECURITY.md).
2. **No fabricated intelligence.** Never hard-code fake threat data,
   fake CVEs, fake researchers, or canned "impressive" results. An empty
   answer must render as `NO RELEVANT PUBLIC INTELLIGENCE FOUND`.
3. **No secrets.** Never commit API keys. Add planned variables to
   `.env.example` with empty values only.
4. **Every verdict is explainable.** If you add a check, it must emit a
   `Finding` with points, an evidence class, and a source; if you add a
   provider, it must be an adapter behind `Provider` with a reliability
   tier.

## Development setup

```bash
git clone <repo> && cd sentiala-shield
python -m venv .venv && source .venv/bin/activate
pip install -e ".[dev]"
pytest
```

The test suite runs fully offline (providers are tested against recorded
synthetic responses using reserved `.test` domains).

## Pull request checklist

- [ ] Tests pass locally: `pytest`
- [ ] New checks/providers have unit tests, including false-positive cases
- [ ] No network calls from unit tests
- [ ] No new dependencies without justification
- [ ] `CHANGELOG.md` updated (Keep a Changelog format)
- [ ] Docs updated if architecture or behaviour changed

## Commit style

Conventional commits (`feat:`, `fix:`, `docs:`, `test:`, `sec:`).

## Code of conduct

See [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md). Be kind; security work is
stressful enough already.
