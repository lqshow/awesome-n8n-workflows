# Awesome n8n Workflows [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated collection of practical n8n workflows for automation enthusiasts

[![GitHub stars](https://img.shields.io/github/stars/lqshow/awesome-n8n-workflows.svg?style=flat-square)](https://github.com/yourusername/awesome-n8n-workflows)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)
[![n8n version](https://img.shields.io/badge/n8n-1.94.1+-blue.svg?style=flat-square)](https://n8n.io/)

- [guardian-agent-prompts](https://github.com/milkomida77/guardian-agent-prompts) - 49 AI agent system prompts for Claude Code with n8n webhook integration for multi-agent orchestration and automated task delegation. MIT licensed.
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

## Contributing

Contributions are welcome! Please ensure your submission includes:

- Workflow JSON file(s)
- Comprehensive README with setup instructions
- Screenshots or demo
- List of dependencies
