# 🔌 MCP 服務器

> 透過 Model Context Protocol 連接外部世界，擴展 OpenCode 的資料存取能力！

## 🎯 MCP 概覽

Model Context Protocol (MCP) 是一個開放標準，允許 AI 應用程式與外部資料來源和工具進行安全互動。透過 MCP，OpenCode 可以存取資料庫、API、檔案系統等外部資源。

### 🏗️ **MCP 架構**

```
🔗 MCP 生態系統
├── 🖥️ MCP 客戶端   (OpenCode)
├── 🔌 MCP 服務器   (資料/工具提供者)
└── 📡 傳輸層       (stdio, HTTP, SSE)

📦 MCP 服務器類型
├── 資料庫服務器    (PostgreSQL, MySQL, MongoDB)
├── 檔案系統服務器  (本地檔案、Google Drive)
├── API 服務器      (GitHub, Slack, Jira)
├── 知識庫服務器    (向量資料庫、文檔搜尋)
└── 工具服務器      (瀏覽器控制、程式執行)
```

## ⚙️ 配置 MCP 服務器

### 🎯 **基本配置**

在 `opencode.json` 中配置 MCP 服務器：

```json
{
  "$schema": "https://opencode.ai/config.json",
  "mcp": {
    "servers": {
      "filesystem": {
        "command": "npx",
        "args": ["-y", "@modelcontextprotocol/server-filesystem", "/path/to/files"]
      }
    }
  }
}
```

### 🎯 **多服務器配置**

```json
{
  "mcp": {
    "servers": {
      "filesystem": {
        "command": "npx",
        "args": ["-y", "@modelcontextprotocol/server-filesystem", "/data"]
      },
      "github": {
        "command": "npx",
        "args": ["-y", "@modelcontextprotocol/server-github"],
        "env": {
          "GITHUB_TOKEN": "${GITHUB_TOKEN}"
        }
      },
      "postgres": {
        "command": "npx",
        "args": ["-y", "@modelcontextprotocol/server-postgres"],
        "env": {
          "DATABASE_URL": "${DATABASE_URL}"
        }
      }
    }
  }
}
```

## 📦 常用 MCP 服務器

### 🗂️ **檔案系統服務器**

```json
{
  "mcp": {
    "servers": {
      "files": {
        "command": "npx",
        "args": [
          "-y",
          "@modelcontextprotocol/server-filesystem",
          "/home/user/projects",
          "/home/user/documents"
        ]
      }
    }
  }
}
```

**功能：**
- 📖 讀取檔案內容
- 📝 寫入和編輯檔案
- 📁 建立和刪除目錄
- 🔍 搜尋檔案

**使用範例：**
```bash
> 請讀取 /home/user/projects/config.json 的內容
> 請在 /home/user/documents 目錄下創建一個新的筆記
```

### 💾 **資料庫服務器**

#### **PostgreSQL**
```json
{
  "mcp": {
    "servers": {
      "postgres": {
        "command": "npx",
        "args": ["-y", "@modelcontextprotocol/server-postgres"],
        "env": {
          "DATABASE_URL": "postgresql://user:pass@localhost:5432/mydb"
        }
      }
    }
  }
}
```

**功能：**
- 🔍 執行 SQL 查詢
- 📊 檢視表結構
- 📈 資料統計分析

**使用範例：**
```bash
> 請查詢 users 表中最近註冊的 10 位用戶
> 請分析 orders 表的銷售趨勢
```

#### **SQLite**
```json
{
  "mcp": {
    "servers": {
      "sqlite": {
        "command": "npx",
        "args": ["-y", "@modelcontextprotocol/server-sqlite", "database.db"]
      }
    }
  }
}
```

### 🐙 **GitHub 服務器**

```json
{
  "mcp": {
    "servers": {
      "github": {
        "command": "npx",
        "args": ["-y", "@modelcontextprotocol/server-github"],
        "env": {
          "GITHUB_TOKEN": "${GITHUB_TOKEN}"
        }
      }
    }
  }
}
```

**功能：**
- 📋 管理 Issues 和 Pull Requests
- 🔍 搜尋程式碼和倉庫
- 📊 查看提交歷史
- 🏷️ 管理標籤和里程碑

**使用範例：**
```bash
> 請列出 my-project 倉庫的所有開放 Issues
> 請創建一個新的 Pull Request
> 請搜尋倉庫中所有包含 TODO 的檔案
```

### 💬 **Slack 服務器**

```json
{
  "mcp": {
    "servers": {
      "slack": {
        "command": "npx",
        "args": ["-y", "@modelcontextprotocol/server-slack"],
        "env": {
          "SLACK_TOKEN": "${SLACK_TOKEN}"
        }
      }
    }
  }
}
```

**功能：**
- 📨 發送訊息
- 🔍 搜尋頻道歷史
- 📋 管理頻道

### 🌐 **瀏覽器服務器**

```json
{
  "mcp": {
    "servers": {
      "puppeteer": {
        "command": "npx",
        "args": ["-y", "@modelcontextprotocol/server-puppeteer"]
      }
    }
  }
}
```

**功能：**
- 🌐 瀏覽網頁
- 📸 截圖
- 🔍 搜尋和提取資訊
- 🖱️ 模擬用戶操作

## 🔧 自定義 MCP 服務器

### 🎯 **開發自己的 MCP 服務器**

使用 TypeScript/JavaScript 創建：

```typescript
// my-mcp-server.ts
import { Server } from "@modelcontextprotocol/sdk/server";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio";

const server = new Server({
  name: "my-custom-server",
  version: "1.0.0"
});

// 定義工具
server.setRequestHandler("tools/list", async () => ({
  tools: [
    {
      name: "get_weather",
      description: "取得指定城市的天氣資訊",
      inputSchema: {
        type: "object",
        properties: {
          city: { type: "string", description: "城市名稱" }
        },
        required: ["city"]
      }
    }
  ]
}));

// 實現工具
server.setRequestHandler("tools/call", async (request) => {
  if (request.params.name === "get_weather") {
    const city = request.params.arguments.city;
    // 呼叫天氣 API...
    return {
      content: [
        { type: "text", text: `${city} 的天氣：晴朗，25°C` }
      ]
    };
  }
});

// 啟動服務器
const transport = new StdioServerTransport();
await server.connect(transport);
```

### 🎯 **配置自定義服務器**

```json
{
  "mcp": {
    "servers": {
      "my-server": {
        "command": "node",
        "args": ["/path/to/my-mcp-server.js"]
      }
    }
  }
}
```

## 🛡️ 安全性考量

### ⚠️ **安全最佳實踐**

1. **最小權限原則**
```json
{
  "mcp": {
    "servers": {
      "files": {
        "args": ["-y", "@modelcontextprotocol/server-filesystem", "/specific/path"]
      }
    }
  }
}
```

2. **環境變數存放敏感資訊**
```json
{
  "env": {
    "DATABASE_URL": "${DATABASE_URL}",
    "API_KEY": "${API_KEY}"
  }
}
```

3. **啟用操作確認**
```json
{
  "mcp": {
    "confirmOperations": true
  }
}
```

## 🔍 故障排除

### ❌ **服務器無法連接**

```bash
# 手動測試服務器
npx -y @modelcontextprotocol/server-filesystem /path

# 檢查日誌
/mcp logs
```

### ❌ **權限錯誤**

```bash
# 確認環境變數已設置
echo $GITHUB_TOKEN

# 確認檔案權限
ls -la /path/to/files
```

---

## 🚀 下一步學習

現在你已經掌握了 MCP 服務器的配置！

👉 **[繼續：插件開發 →](plugins.md)**

---

<div align="center">
  <p><strong>🔌 連接無限可能！</strong></p>
  <p>💡 訣竅：MCP 讓 AI 能夠存取你的資料，大幅提升生產力</p>
</div>
