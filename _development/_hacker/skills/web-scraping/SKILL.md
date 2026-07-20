---
name: web-scraping
description: >
  Extract structured data from websites politely and reliably, including
  JavaScript-rendered pages, using the Playwright MCP browser. Trigger whenever
  the task is to "scrape", "crawl", "extract data from a site", "collect
  listings/prices/results", or automate reading a web page. Teaches ethical and
  technical practice: check what you are allowed to collect, discover the site
  structure, drive a real browser for dynamic content, throttle politely, and
  keep the extracted data clean.
---

# Web scraping

This skill makes you a careful, effective web scraper. You drive a real
browser through the **Playwright MCP** server configured for this use case,
which lets you handle JavaScript-rendered pages, logins, and dynamic content
that a plain HTTP client cannot.

Read the `_hacker` rules of engagement first — scraping is subject to the
authorization and conduct rules there, especially rule 8 (respect
`robots.txt`, rate limits, and terms of service).

## Step 0 — Confirm you are allowed to collect this

Before the first request:

- Check `robots.txt` and the site's terms of service. If either forbids the
  access you intend, stop and tell the developer.
- Identify whether the data includes personal data. If it does, confirm you
  are authorized to process it; otherwise do not collect it.
- Decide a polite request rate and stick to it. Default to slow.

## Step 1 — Map the site before extracting

- Read `robots.txt` and any `sitemap.xml` to learn the intended structure and
  which paths are off-limits.
- Load a representative page and inspect the DOM to find the stable selectors
  (prefer IDs, `data-*` attributes, and semantic structure over brittle
  nth-child chains).
- Determine how the content loads: server-rendered HTML, XHR/fetch JSON, or
  client-side rendering. If the data arrives as a JSON API response, prefer
  reading that response directly over scraping the rendered DOM — it is more
  stable and lighter on the site.

## Step 2 — Extract with the right tool for the page

- **Static / server-rendered pages:** fetch and parse the HTML.
- **Dynamic / JS-rendered pages:** use Playwright MCP to navigate, wait for the
  content to settle (wait for the specific element or network idle, not a
  fixed sleep), then read the page or the network responses.
- **Paginated or infinite-scroll lists:** iterate pages or scroll in a loop
  with a bounded stop condition; never loop unbounded.
- **Auth-gated content:** only when authorized. Log in through the normal flow;
  never hardcode or exfiltrate credentials (see rules 4–5).

## Step 3 — Be a polite client

- Throttle: insert a delay between requests and cap concurrency. When the site
  publishes a crawl-delay or rate limit, obey it.
- Fail gracefully: back off on `429`/`503`, honour `Retry-After`, and stop
  after repeated errors rather than hammering.
- Identify honestly. Do not impersonate another client to evade controls.

## Step 4 — Keep the data clean

- Extract into a defined schema; validate types and required fields as you go.
- Deduplicate on a stable key and record provenance (source URL, fetch time).
- Store secrets or personal data by kind and location only if they appear
  incidentally — do not retain the values (rule 4).

## Step 5 — Report

Tell the developer: what was collected, the schema, how many records, which
pages/paths were skipped and why, and any rate-limiting or blocking you hit.
