# 🎨 Pixel Sensei - AI 技术漫画生成器

> 将复杂的技术概念转化为生动有趣的漫画故事，让学习变得轻松愉快

📖 **[完整教程](https://mulerun.com/@LunarAITalk/pixelsensei)** | 🎯 **技术栈**: n8n + Langchain Agent + Google Gemini API

## 🚀 快速开始

### 📦 核心功能

| 功能模块 | 说明 | 特点 | 使用场景 |
|----------|------|------|----------|
| **AI 规划引擎** | 智能分析技术主题 | 自动拆解概念、设计故事线 | 任意技术概念教学 |
| **角色对话系统** | 多角色互动教学 | Rick & Morty、变形金刚、蝙蝠侠 | 趣味化知识传递 |
| **漫画风格引擎** | 多种艺术风格 | manga、minimal、cyberpunk、sketch | 个性化内容呈现 |
| **HTML 渲染器** | 精美页面输出 | 响应式设计、主题切换 | 分享与展示 |

### 📥 工作流文件

- `PixelSensei(ZH).json` - AI 技术漫画生成器工作流

## ✨ 核心特性

- 🤖 **AI 智能规划**: 自动分析技术主题复杂度，生成合适的漫画页数和故事结构
- 🎭 **多角色系统**: 支持 Rick & Morty、Optimus & Bumblebee、Batman & Robin 等经典角色对
- 🎨 **多种艺术风格**: manga（日漫）、minimal（极简）、cyberpunk（赛博朋克）、sketch（手绘）
- 📖 **故事驱动学习**: 通过问题→探索→解决的叙事弧线，让知识点自然融入故事
- 🌐 **精美 HTML 输出**: 响应式设计，支持主题切换，方便分享和嵌入
- 🌍 **多语言支持**: 自动检测输入语言，支持中英文内容生成

## 🛠 依赖工具

- [n8n](https://n8n.io) - 工作流自动化平台
- Google Gemini API - AI 内容生成与图像生成
- Langchain Agent - AI 智能代理框架

## 🎬 使用示例

### 输入示例
```
主题: Kubernetes Pod 生命周期
角色: Rick & Morty
风格: manga
```

### 输出效果
- 自动生成 5-15 页漫画（根据主题复杂度）
- 每页包含角色对话、技术讲解、学习要点
- 输出精美的 HTML 页面，可直接分享

## 🔧 部署配置

### 1. 环境准备
```bash
# 启动 n8n
docker run -it --rm \
    --name n8n \
    -p 5678:5678 \
    -v n8n_data:/home/node/.n8n \
    docker.n8n.io/n8nio/n8n
```

### 2. 工作流配置
1. 导入 `PixelSensei(ZH).json` 工作流
2. 配置 Google Gemini API 凭证
3. 配置 Langchain Agent 节点
4. 激活工作流，开始生成漫画

### 3. 支持的角色对

| 角色对 | 导师 | 学习者 | 教学风格 |
|--------|------|--------|----------|
| **Rick & Morty** | Rick Sanchez | Morty Smith | 科幻比喻、跨维度类比 |
| **Transformers** | Optimus Prime | Bumblebee | 变形机制、模块化系统 |
| **Batman & Robin** | Batman | Robin | 侦探逻辑、证据分析 |

---

*用漫画讲述技术故事，让复杂概念变得生动有趣！*
