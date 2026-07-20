# _development/_hacker

**Choose this use case (in addition to `_development`) when** the agent being
created needs to do **hacking or security work**, or must build a **deep,
adversarial understanding of a third-party or untrusted web system**.
Recognition signals: "pentest", "penetration test", "security assessment",
"find vulnerabilities", "XSS / SQLi / auth bypass", "bug bounty", "scrape a
site", "recon", "understand someone else's web app or API".

Web-focused by design: authorized web reconnaissance, scraping, and
web-application penetration testing. It does **not** cover general reverse
engineering.

## What it provides

- `.agents/.mcp.json` — official Playwright MCP (browser automation) in
  standard `.mcp.json` format, portable across models.
- `AGENTS.md` — rules of engagement: authorized-scope-only, least-invasive
  first, secrets recorded by kind and location only, reproducible evidence, and
  polite scraping.
- Skills: `web-scraping`, `web-pentest`.

## Distinction from `_brownfield`

`_brownfield` is for developing a codebase you have access to. `_hacker` is for
security-driven, adversarial understanding and testing of systems you are
**authorized** to assess.
