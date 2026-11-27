# Awesome n8n Workflows [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated collection of practical n8n workflows for automation enthusiasts

[![GitHub stars](https://img.shields.io/github/stars/lqshow/awesome-n8n-workflows.svg?style=flat-square)](https://github.com/yourusername/awesome-n8n-workflows)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)
[![n8n version](https://img.shields.io/badge/n8n-1.94.1+-blue.svg?style=flat-square)](https://n8n.io/)

## Workflows

### 📂 [GitHub to Feishu Collector](./workflows/github-to-feishu-collector/)

One-click collection of GitHub project information to a Feishu Bitable using a browser extension.

**Key Features**: Browser extension, one-click trigger, stable data via GitHub API, automatic sync to Feishu.

**Tech Stack**: n8n + GitHub API + Feishu Bitable

### 💬 [WeChat AI Daily Report Generator](./workflows/wechat-daily-report/)

Automatically analyze WeChat group chat records and generate beautiful HTML daily reports powered by AI.

**Key Features**: AI content analysis, data visualization, mobile-responsive design, batch processing

**Tech Stack**: n8n + ChatlogMCP + Google Gemini + EdgeOne Pages

### 🧠 [RAG Knowledge Assistant](./workflows/rag-knowledge-assistant/)

Build a local RAG system that transforms static documents into an intelligent conversational assistant, eliminating AI hallucinations with fact-based responses.

**Key Features**: Document processing, semantic search, multi-format support, local deployment, privacy protection

**Tech Stack**: n8n + Ollama + Qwen3-Embedding + Vector Store

### 🌍 [Multi-Language Translator](./workflows/multi-language-translator/)

AI-powered translation service with RESTful API interface, supporting real-time translation between 6 major languages with structured JSON responses.

**Key Features**: Multi-language support, batch translation, error handling, structured responses, webhook integration

**Tech Stack**: n8n + Google Gemini CLI + Webhook

### 📰 [Xiaobot Article Harvester](./workflows/xiaobot-article-harvester/)

Automatically harvest and download articles from Xiaobot columns, converting them to Markdown format with intelligent browser automation that bypasses dynamic API signatures.

**Key Features**: Browser automation, API interception, batch article download, HTML to Markdown conversion, smart file naming

**Tech Stack**: n8n + Crawl4AI + Browser Automation

### [Arcmira YouTube transcript source shortlist](./workflows/arcmira-source-shortlist/)

Find up to three timestamped passages in indexed YouTube videos, with source links and coverage notes. Includes a [real CLI demo](./workflows/arcmira-source-shortlist/DEMO.md).

**Tech Stack**: n8n built-in nodes + [Arcmira API](https://arcmira.com/docs). An [Arcmira](https://arcmira.com) account is required; limited free access and paid plans are available. Workflow and documentation retain Apache-2.0.

### [Self-Hosted n8n Webhook Starter Pack](./workflows/self-hosted-webhook-starter-pack/)

Five self-hosted n8n workflows covering payment webhooks, AI SEO brief generation, an OpenClaw Telegram assistant, uptime/SSL/price monitoring, and a confidence-gated RAG support bot. Includes [curl webhook tests and expected JSON outputs](./workflows/self-hosted-webhook-starter-pack/DEMO.md).

**Key Features**: Built-in n8n nodes only, `$env.*` secret hygiene, deterministic JSON webhook responses, Telegram chat ID allowlisting, confidence-gated human escalation

**Tech Stack**: n8n built-in nodes + OpenAI-compatible LLM APIs + Telegram Bot API + Google Sheets + Notion API + OpenClaw Gateway. MIT-licensed upstream stack at [tunguyen1993/vn-ai-vps-stack](https://github.com/tunguyen1993/vn-ai-vps-stack).

### [B2B Market Intel & AI RAG Starter Pack](./workflows/b2b-market-intel-mcp-pack/)

Five zero-key n8n workflows built exclusively with built-in n8n nodes (`manualTrigger`, `scheduleTrigger`, `httpRequest`, `code`, `if`, `stickyNote`) querying live public APIs: UK Contracts Finder OCDS tenders, ClinicalTrials.gov v2 biotech sponsor leads, WooCommerce/WordPress 1-star churn RSS, Google News `CBMi`/`AU_yqL` real-publisher URL decoding (`Fbv4je`), and Open-VSX Cursor/Windsurf extension bug reviews. Includes [verified live curl checks and outputs](./workflows/b2b-market-intel-mcp-pack/DEMO.md).

**Key Features**: Zero API keys required, built-in n8n nodes only, MIT-licensed workflows & documentation, optional MCP/Python SDK/Apify scale-up notes

**Tech Stack**: Built-in n8n nodes + Contracts Finder OCDS + ClinicalTrials.gov v2 + WordPress.org API/RSS + Google News `Fbv4je` + Open-VSX API (MIT license; optional [b2b-market-intel-mcp](https://github.com/truonggiang0111/b2b-market-intel-mcp) & [b2b-market-intel-python](https://github.com/truonggiang0111/b2b-market-intel-python)).

## Contributing

Contributions are welcome! Please ensure your submission includes:

- Workflow JSON file(s)
- Comprehensive README with setup instructions
- Screenshots or demo
- List of dependencies
