# 🤖 模型配置

> 掌握 OpenCode 的模型配置系統，選擇最適合你的 AI 模型！

## 🎯 模型系統概覽

OpenCode 支援 **75+ 個 LLM 提供商**，從 OpenAI、Anthropic、Google 到本地模型，讓你能夠根據不同需求選擇最適合的 AI 模型。

### 🏢 **支援的主要提供商**

```
☁️ 雲端服務
├── OpenAI         (GPT-4o, GPT-4 Turbo, o1, o3)
├── Anthropic      (Claude 4, Claude Sonnet, Claude Haiku)
├── Google         (Gemini 2.0, Gemini Pro)
├── Microsoft      (Azure OpenAI)
├── AWS            (Bedrock)
└── Mistral        (Mistral Large, Mixtral)

🖥️ 本地運行
├── Ollama         (Llama 3, CodeLlama, Mistral)
├── LM Studio      (各種開源模型)
└── LocalAI        (自定義模型)

🔗 代理服務
├── OpenRouter     (統一接口存取多個提供商)
├── Together AI    (開源模型平台)
└── Custom         (自定義 API 端點)
```

## ⚙️ 基本配置

### 🎯 **使用 /connect 命令**

```bash
# 啟動 OpenCode
opencode

# 開始配置模型
/connect
```

系統將引導你完成配置：

```
🔧 選擇提供商：
  [1] OpenAI
  [2] Anthropic
  [3] Google Gemini
  [4] Ollama (本地)
  [5] 其他...

請輸入數字選擇：1

🔑 輸入 API 金鑰：
sk-proj-xxxxxxxxxxxxx

🤖 選擇預設模型：
  [1] gpt-4o (推薦)
  [2] gpt-4-turbo
  [3] gpt-4o-mini
  [4] o1
  [5] o3-mini

請輸入數字選擇：1

✅ 配置完成！模型已設定為 openai/gpt-4o
```

### 🎯 **手動配置文件**

在 `opencode.json` 中配置：

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "default": "anthropic",
    "anthropic": {
      "apiKey": "${ANTHROPIC_API_KEY}",
      "model": "claude-sonnet-4-5"
    }
  }
}
```

## 🏢 提供商詳細配置

### 💚 **OpenAI 配置**

```json
{
  "provider": {
    "openai": {
      "apiKey": "${OPENAI_API_KEY}",
      "model": "gpt-4o",
      "organization": "org-xxxx",
      "baseUrl": "https://api.openai.com/v1"
    }
  }
}
```

**可用模型：**
| 模型 | 特點 | 適用場景 |
|------|------|----------|
| `gpt-4o` | 最強多模態 | 複雜編程、圖片理解 |
| `gpt-4o-mini` | 快速便宜 | 日常開發任務 |
| `o1` | 深度推理 | 演算法設計、數學問題 |
| `o3-mini` | 推理+速度 | 複雜分析、快速回應 |

### 🧡 **Anthropic 配置**

```json
{
  "provider": {
    "anthropic": {
      "apiKey": "${ANTHROPIC_API_KEY}",
      "model": "claude-sonnet-4-5",
      "maxTokens": 8192
    }
  }
}
```

**可用模型：**
| 模型 | 特點 | 適用場景 |
|------|------|----------|
| `claude-sonnet-4-5` | 平衡能力 | 日常開發（推薦） |
| `claude-4-opus` | 最強推理 | 複雜架構設計 |
| `claude-haiku-3` | 極速回應 | 快速問答 |

### 💙 **Google Gemini 配置**

```json
{
  "provider": {
    "google": {
      "apiKey": "${GOOGLE_API_KEY}",
      "model": "gemini-2.0-flash",
      "safetySettings": "balanced"
    }
  }
}
```

**可用模型：**
| 模型 | 特點 | 適用場景 |
|------|------|----------|
| `gemini-2.0-flash` | 快速多模態 | 圖片處理、快速開發 |
| `gemini-2.0-pro` | 強大推理 | 複雜任務 |
| `gemini-1.5-pro` | 超長上下文 | 大型代碼庫分析 |

### 🦙 **Ollama 本地配置**

```json
{
  "provider": {
    "ollama": {
      "baseUrl": "http://localhost:11434",
      "model": "llama3:70b"
    }
  }
}
```

**推薦本地模型：**
| 模型 | VRAM 需求 | 適用場景 |
|------|-----------|----------|
| `llama3:8b` | 8GB | 輕量開發 |
| `llama3:70b` | 40GB+ | 完整功能 |
| `codellama:34b` | 24GB | 代碼專精 |
| `deepseek-coder:33b` | 24GB | 代碼生成 |

## 🔄 多模型配置

### 🎯 **按任務分配模型**

```json
{
  "provider": {
    "default": "anthropic",
    "anthropic": {
      "model": "claude-sonnet-4-5"
    }
  },
  "agent": {
    "main": {
      "model": "anthropic/claude-sonnet-4-5"
    },
    "subagent": {
      "model": "openai/gpt-4o-mini"
    },
    "planner": {
      "model": "openai/o1"
    }
  }
}
```

### 🎯 **備援模型配置**

```json
{
  "provider": {
    "default": "openai",
    "fallback": ["anthropic", "google"]
  }
}
```

當主模型失敗時，自動切換到備援模型。

## 🎚️ 進階參數調整

### 🎯 **模型參數說明**

```json
{
  "model": {
    "temperature": 0.7,
    "maxTokens": 4096,
    "topP": 0.95,
    "frequencyPenalty": 0,
    "presencePenalty": 0
  }
}
```

| 參數 | 範圍 | 說明 |
|------|------|------|
| `temperature` | 0-2 | 創造力，越高越隨機 |
| `maxTokens` | 1-128K | 最大回應長度 |
| `topP` | 0-1 | 核心採樣，影響多樣性 |
| `frequencyPenalty` | -2 to 2 | 減少重複用詞 |
| `presencePenalty` | -2 to 2 | 鼓勵新話題 |

### 🎯 **任務導向參數**

```json
{
  "model": {
    "profiles": {
      "coding": {
        "temperature": 0.2,
        "maxTokens": 8192
      },
      "creative": {
        "temperature": 0.9,
        "maxTokens": 4096
      },
      "analysis": {
        "temperature": 0.3,
        "maxTokens": 16384
      }
    }
  }
}
```

## 💰 成本優化

### 🎯 **模型價格比較（2026 參考）**

| 模型 | 輸入 (每 1M tokens) | 輸出 (每 1M tokens) |
|------|---------------------|---------------------|
| GPT-4o | $5 | $15 |
| GPT-4o-mini | $0.15 | $0.60 |
| Claude Sonnet | $3 | $15 |
| Gemini 2.0 Flash | $0.075 | $0.30 |
| Llama 3 (本地) | 免費 | 免費 |

### 🎯 **成本優化策略**

```json
{
  "costOptimization": {
    "enabled": true,
    "strategy": "auto",
    "rules": [
      {
        "task": "simple-question",
        "model": "gpt-4o-mini"
      },
      {
        "task": "code-generation",
        "model": "claude-sonnet-4-5"
      },
      {
        "task": "architecture-design",
        "model": "o1"
      }
    ]
  }
}
```

## 🔧 故障排除

### ❌ **API 金鑰錯誤**

```bash
# 錯誤訊息
Error: Invalid API key

# 檢查金鑰
echo $OPENAI_API_KEY

# 重新設定
export OPENAI_API_KEY="sk-proj-xxxx"

# 或使用 /connect 重新配置
/connect
```

### ❌ **模型不可用**

```bash
# 錯誤訊息
Error: Model not found

# 解決：檢查模型名稱拼寫
# 正確：claude-sonnet-4-5
# 錯誤：claude-sonnet-4.5

# 使用 /models 查看可用模型
/models
```

### ❌ **速率限制**

```bash
# 錯誤訊息
Error: Rate limit exceeded

# 解決方案 1：等待重試
# 解決方案 2：切換備援模型
# 解決方案 3：升級 API 計劃
```

---

## 🚀 下一步學習

現在你已經掌握了 OpenCode 的模型配置！

👉 **[繼續：自定義工具 →](custom-tools.md)**

---

<div align="center">
  <p><strong>🤖 選對模型，事半功倍！</strong></p>
  <p>💡 訣竅：日常開發用 claude-sonnet，複雜推理用 o1</p>
</div>
