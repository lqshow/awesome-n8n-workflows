# 🎬 VideoUpscaler — 4K AI Video Super-Resolution Pipeline

> Automated 1080p / 2K / 4K AI video super-resolution workflow powered by FlashVSR diffusion upscaling, with zero-flicker temporal consistency and original audio preservation

📖 **[Integration Hub](https://videoupscaler.co/integrations)** | 📚 **[Workflow Guide](https://videoupscaler.co/docs/workflows)** | 📦 **[npm: `n8n-nodes-videoupscaler`](https://www.npmjs.com/package/n8n-nodes-videoupscaler)** | 🎯 **Tech Stack**: n8n + VideoUpscaler API (`FlashVSR`) + Webhook / Long-Polling

## 🚀 Quick Start

### 📦 Core Modules

| Module | Description | Highlights | Use Case |
|--------|-------------|------------|----------|
| **HTTP Long-Polling Pipeline** | Built-in `HTTP Request` + `?wait=45` loop | Works on n8n Cloud & self-hosted with zero custom nodes | Upscaling AI-generated clips (Sora, Runway, Kling, Veo) to 4K |
| **Async Webhook Pipeline** | Zero-polling event callback (`task.completed`) | Instant HTTP POST callback when 4K MP4 is ready | Batch video enhancement & long-form media pipelines |
| **Official Community Node** | [`n8n-nodes-videoupscaler`](https://www.npmjs.com/package/n8n-nodes-videoupscaler) | Single-node 4K upscale with automatic waiting | Self-hosted n8n media automation |

### 📥 Workflow Files

- `n8n-videoupscaler-workflow.json` - Self-documenting HTTP Request + server-side long-polling (`?wait=45`) workflow (n8n Cloud & Self-Hosted)
- `n8n-videoupscaler-webhook-workflow.json` - Async webhook callback pipeline (`X-VideoUpscaler-Event: task.completed`) for batch & long videos
- `n8n-videoupscaler-node-workflow.json` - 3-node workflow using the official [`n8n-nodes-videoupscaler`](https://www.npmjs.com/package/n8n-nodes-videoupscaler) community node

## ✨ Key Features

- 🎞️ **Diffusion Video Super-Resolution (FlashVSR)**: Generates realistic textures (skin, hair, fabric, foliage) with temporal consistency across frames instead of frame-by-frame flickering
- 🔊 **Original Audio Preserved**: Outputs H.264 MP4 in `1080p`, `2k`, or `4k` with the source audio stream intact
- ⚡ **Server-Side Long Polling (`?wait=45`)**: Holds the status request open up to 45 seconds per cycle, drastically reducing n8n execution steps
- 🔔 **Async Webhook Callbacks**: Pass `webhook_url` to receive an instant `POST` notification when rendering finishes
- 🛡️ **Idempotent Execution**: Uses `Idempotency-Key: {{ $execution.id }}` so workflow retries never double-charge credits

## 🛠 Dependencies

- [n8n](https://n8n.io) (Cloud or Self-Hosted `>=1.0.0`)
- [VideoUpscaler API Key](https://videoupscaler.co/settings/apikeys) (`Bearer vu_live_...`)
- Optional (Self-Hosted): [`n8n-nodes-videoupscaler`](https://www.npmjs.com/package/n8n-nodes-videoupscaler) community node ([GitHub](https://github.com/arkyu2077/n8n-nodes-videoupscaler))

## 🎬 Usage Example

### Input Payload
```json
{
  "video_url": "https://example.com/ai-generated-clip.mp4",
  "resolution": "4k"
}
```

### Output Payload
```json
{
  "id": "tsk_01j...",
  "status": "completed",
  "resolution": "4k",
  "output_url": "https://cdn.videoupscaler.co/outputs/tsk_01j.../4k.mp4",
  "credits_cost": 15,
  "duration_seconds": 5
}
```

## 🔧 Setup Instructions

1. Import `n8n-videoupscaler-workflow.json` into your n8n canvas (**Workflows → Import from File**).
2. Create an API key (`vu_live_...`) at [videoupscaler.co/settings/apikeys](https://videoupscaler.co/settings/apikeys).
3. In the **Start Upscale** and **Poll Task** nodes, configure a **Header Auth** credential:
   - **Name**: `Authorization`
   - **Value**: `Bearer vu_live_YOUR_API_KEY`
4. Or on self-hosted n8n, install [`n8n-nodes-videoupscaler`](https://www.npmjs.com/package/n8n-nodes-videoupscaler) via **Settings → Community Nodes** and import `n8n-videoupscaler-node-workflow.json`.
