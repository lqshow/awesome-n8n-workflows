# Awesome n8n Workflows [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated collection of practical n8n workflows for automation enthusiasts

[![GitHub stars](https://img.shields.io/github/stars/lqshow/awesome-n8n-workflows.svg?style=flat-square)](https://github.com/yourusername/awesome-n8n-workflows)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)
[![n8n version](https://img.shields.io/badge/n8n-1.94.1+-blue.svg?style=flat-square)](https://n8n.io/)

## Workflows

# 📂 [Solana Mint/Program Monitor](./workflows/solana-mint-monitor/)

Watches an SPL mint or program ID via public RPC and alerts on Telegram when a new transaction appears.

**Key Features**: No external database, public RPC only, 5-minute setup, free and MIT-licensed.

**Tech Stack**: n8n + Solana public RPC + Telegram

More free n8n workflow packs: https://negozio.91.99.198.106.sslip.io/?src=lqshow-awesome-n8n-workflows


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

## Contributing

Contributions are welcome! Please ensure your submission includes:

- Workflow JSON file(s)
- Comprehensive README with setup instructions
- Screenshots or demo
- List of dependencies
