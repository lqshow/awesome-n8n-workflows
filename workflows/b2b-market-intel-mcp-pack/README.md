# B2B Market Intel & AI RAG Starter Pack (Zero-Key Built-In n8n Nodes)

A pack of **5 self-contained n8n workflows** built strictly with **built-in n8n nodes** (`manualTrigger`, `scheduleTrigger`, `httpRequest`, `code`, `if`, `stickyNote`) — zero credentials, zero API keys, and zero third-party community packages required.

Every workflow targets live, public, zero-key REST/RSS/OCDS endpoints so you can import the `.json` file into n8n and click **Test Workflow** immediately.

## License & Node Disclosure

- **License:** MIT License (`truonggiang0111`)
- **Nodes Used:** Built-in n8n core nodes only (`manualTrigger`, `scheduleTrigger`, `httpRequest`, `code`, `if`, `stickyNote`).
- **Credentials Required:** None (`$0` upfront, zero API keys).

## Included Workflows

| # | File | Triggers | Public Zero-Key Endpoint | Output / Use Case |
| :- | :--- | :--- | :--- | :--- |
| 01 | [`01_uk_gov_contracts_finder_b2b_tenders.json`](./01_uk_gov_contracts_finder_b2b_tenders.json) | Manual + Daily Schedule | `contractsfinder.service.gov.uk/Published/Notices/OCDS/Search` | UK public-sector tenders & awards with buyer orgs, `.gov.uk`/NHS contact emails, GBP values, deadlines, and official notice URLs. |
| 02 | [`02_clinicaltrials_biotech_sponsor_leads.json`](./02_clinicaltrials_biotech_sponsor_leads.json) | Manual + Daily Schedule | `clinicaltrials.gov/api/v2/studies` | Actively recruiting Industry-sponsored biotech/pharma clinical trials with NCT ID, sponsor name, phases, enrollment, and central contacts. |
| 03 | [`03_wordpress_woocommerce_1star_churn_monitor.json`](./03_wordpress_woocommerce_1star_churn_monitor.json) | Manual + Daily Schedule | `api.wordpress.org/plugins/info/1.2/` + `wordpress.org/support/plugin/<slug>/reviews/feed/?filter=1` | Scores WooCommerce/WordPress plugins by 1–2★ ratio & unresolved threads, then classifies live 1★ complaint RSS items (`billing_pricing`, `bugs_breakage`, `support_churn`). |
| 04 | [`04_google_news_real_url_rag_decoder.json`](./04_google_news_real_url_rag_decoder.json) | Manual + Daily Schedule | `news.google.com/rss/search` + `DotsSplashUi/data/batchexecute?rpcids=Fbv4je` | Decodes `CBMi` (offline protobuf fast-path) and modern `AU_yqL` Google News wrapper URLs into canonical publisher URLs for AI RAG ingestion. |
| 05 | [`05_openvsx_cursor_extension_bug_spy.json`](./05_openvsx_cursor_extension_bug_spy.json) | Manual + Daily Schedule | `open-vsx.org/api/-/search` + `/api/<ns>/<name>/reviews` | Surfaces high-install Cursor/Windsurf AI & MCP extensions and extracts `<= 3★` developer bug/UX reviews. |

## Setup in 60 Seconds

1. Open n8n -> **Workflows** -> **Import from File** (or copy raw JSON from GitHub).
2. Click **Test Workflow Manually** — no credential configuration is needed.
3. Optionally adjust parameters (keywords, conditions, plugin slug, or query size) inside the first `Configure ...` **Code** node.
4. Connect the final `Code` output node to Slack, Notion, Google Sheets, HubSpot, or Postgres/Qdrant.

## Live Demo & Verification

See [`DEMO.md`](./DEMO.md) for runnable `curl` commands and observed live outputs from all five zero-key endpoints.

## Optional MCP, Python SDK & Scaled Cloud Batch Notes

If you also want to call these workflows from **AI coding agents** (Claude Code, Cursor, Windsurf, VS Code) or scale past local IP rate limits on large batches (`50–1,000+` items, full article Markdown, cross-store App Store + Google Play + Shopify reviews):

- **Zero-Key Node.js STDIO MCP Server (MIT):** `npx -y github:truonggiang0111/b2b-market-intel-mcp` ([GitHub](https://github.com/truonggiang0111/b2b-market-intel-mcp))
- **Zero-Dependency Python 3.10+ Stdlib CLI & SDK (MIT):** [truonggiang0111/b2b-market-intel-python](https://github.com/truonggiang0111/b2b-market-intel-python) (`uvx --from git+https://github.com/truonggiang0111/b2b-market-intel-python b2b-intel --self-test`)
- **Standalone Google News `CBMi` / `AU_yqL` CLI (MIT):** [truonggiang0111/google-news-url-decoder](https://github.com/truonggiang0111/google-news-url-decoder)
- **Hosted One-Click Agent Skills (Agensi):** [agensi.io/creators/giang-tr-ng-tr-ng](https://www.agensi.io/creators/giang-tr-ng-tr-ng) (includes Free Google News Decoder & App Bug Review skills)
- **Hosted Cloud Batch Actors (`$5/mo` free Apify tier):** [apify.com/ttyan0111](https://apify.com/ttyan0111) & [MCP Docs Hub](https://truonggiang0111.github.io/mcp/)
