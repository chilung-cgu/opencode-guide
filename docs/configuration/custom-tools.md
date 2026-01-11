# 🔧 自定義工具

> 擴展 OpenCode 的能力，創建屬於你的專屬工具！

## 🎯 自定義工具概覽

OpenCode 的自定義工具系統讓你可以擴展 AI 的能力範圍。你可以創建專屬工具，讓 AI 與外部系統互動、執行特定任務，或整合專有流程。

### 🏗️ **工具類型**

```
🛠️ 自定義工具
├── 命令工具      (執行系統命令)
├── API 工具      (呼叫外部 API)
├── 腳本工具      (執行自定義腳本)
├── 整合工具      (第三方服務整合)
└── 資料工具      (資料處理和轉換)
```

## ⚙️ 基本工具創建

### 🎯 **配置文件方式**

在 `opencode.json` 中定義工具：

```json
{
  "$schema": "https://opencode.ai/config.json",
  "tools": {
    "deploy": {
      "description": "部署應用到生產環境",
      "command": "npm run deploy",
      "workingDir": "${workspaceFolder}",
      "confirm": true
    }
  }
}
```

### 🎯 **工具定義結構**

```json
{
  "tools": {
    "工具名稱": {
      "description": "工具功能描述",
      "command": "執行的命令",
      "workingDir": "工作目錄",
      "env": {
        "環境變數": "值"
      },
      "args": ["參數1", "參數2"],
      "confirm": true,
      "timeout": 30000
    }
  }
}
```

## 📋 實用工具範例

### 🎯 **開發工具**

#### **測試工具**
```json
{
  "tools": {
    "test": {
      "description": "執行所有測試",
      "command": "npm test",
      "confirm": false
    },
    "test-coverage": {
      "description": "執行測試並生成覆蓋率報告",
      "command": "npm run test:coverage",
      "confirm": false
    },
    "test-watch": {
      "description": "監視模式執行測試",
      "command": "npm run test:watch",
      "confirm": false
    }
  }
}
```

#### **程式碼品質工具**
```json
{
  "tools": {
    "lint": {
      "description": "檢查程式碼風格",
      "command": "npm run lint",
      "confirm": false
    },
    "format": {
      "description": "格式化程式碼",
      "command": "npx prettier --write .",
      "confirm": true
    },
    "typecheck": {
      "description": "TypeScript 類型檢查",
      "command": "npx tsc --noEmit",
      "confirm": false
    }
  }
}
```

### 🎯 **部署工具**

```json
{
  "tools": {
    "deploy-staging": {
      "description": "部署到測試環境",
      "command": "npm run deploy:staging",
      "env": {
        "NODE_ENV": "staging"
      },
      "confirm": true
    },
    "deploy-production": {
      "description": "部署到生產環境",
      "command": "npm run deploy:prod",
      "env": {
        "NODE_ENV": "production"
      },
      "confirm": true
    }
  }
}
```

### 🎯 **資料庫工具**

```json
{
  "tools": {
    "db-migrate": {
      "description": "執行資料庫遷移",
      "command": "npx prisma migrate dev",
      "confirm": true
    },
    "db-seed": {
      "description": "填充測試資料",
      "command": "npx prisma db seed",
      "confirm": true
    },
    "db-studio": {
      "description": "開啟資料庫管理界面",
      "command": "npx prisma studio",
      "confirm": false
    }
  }
}
```

## 🔗 API 工具創建

### 🎯 **基本 API 工具**

```json
{
  "tools": {
    "check-api-status": {
      "description": "檢查 API 服務狀態",
      "type": "http",
      "method": "GET",
      "url": "https://api.yourservice.com/health",
      "headers": {
        "Authorization": "Bearer ${API_TOKEN}"
      }
    }
  }
}
```

### 🎯 **POST 請求工具**

```json
{
  "tools": {
    "create-issue": {
      "description": "在 GitHub 創建 Issue",
      "type": "http",
      "method": "POST",
      "url": "https://api.github.com/repos/${REPO}/issues",
      "headers": {
        "Authorization": "token ${GITHUB_TOKEN}",
        "Accept": "application/vnd.github.v3+json"
      },
      "body": {
        "title": "${title}",
        "body": "${body}",
        "labels": ["bug"]
      }
    }
  }
}
```

## 📜 腳本工具

### 🎯 **Shell 腳本工具**

創建 `.opencode/tools/cleanup.sh`：

```bash
#!/bin/bash
# 清理專案暫存檔案

echo "🧹 開始清理..."

# 清理 node_modules
rm -rf node_modules/.cache

# 清理建置產物
rm -rf dist build .next

# 清理日誌檔案
find . -name "*.log" -delete

# 清理暫存檔案
find . -name ".DS_Store" -delete

echo "✅ 清理完成！"
```

配置工具：

```json
{
  "tools": {
    "cleanup": {
      "description": "清理專案暫存檔案",
      "command": "bash .opencode/tools/cleanup.sh",
      "confirm": true
    }
  }
}
```

### 🎯 **Python 腳本工具**

創建 `.opencode/tools/analyze.py`：

```python
#!/usr/bin/env python3
"""分析專案程式碼統計"""

import os
from pathlib import Path

def count_lines(directory: str, extensions: list) -> dict:
    stats = {}
    for ext in extensions:
        files = list(Path(directory).rglob(f"*{ext}"))
        total_lines = sum(
            len(f.read_text().splitlines()) 
            for f in files 
            if f.is_file()
        )
        stats[ext] = {
            "files": len(files),
            "lines": total_lines
        }
    return stats

if __name__ == "__main__":
    stats = count_lines("src", [".ts", ".tsx", ".js", ".jsx"])
    
    print("📊 程式碼統計")
    print("-" * 40)
    for ext, data in stats.items():
        print(f"{ext}: {data['files']} 檔案, {data['lines']} 行")
```

配置：

```json
{
  "tools": {
    "analyze": {
      "description": "分析專案程式碼統計",
      "command": "python3 .opencode/tools/analyze.py",
      "confirm": false
    }
  }
}
```

## 🔄 工具組合

### 🎯 **工作流程工具**

```json
{
  "tools": {
    "pre-commit": {
      "description": "提交前檢查（格式化 + Lint + 測試）",
      "command": "npm run format && npm run lint && npm test",
      "confirm": true
    },
    "full-check": {
      "description": "完整品質檢查",
      "command": "npm run lint && npm run typecheck && npm run test:coverage",
      "confirm": false
    },
    "release": {
      "description": "發布新版本",
      "command": "npm run build && npm run test && npm publish",
      "confirm": true
    }
  }
}
```

## 🔐 安全最佳實踐

### ⚠️ **安全注意事項**

1. **使用環境變數存放敏感資訊**
```json
{
  "tools": {
    "deploy": {
      "env": {
        "API_KEY": "${SECRET_API_KEY}"
      }
    }
  }
}
```

2. **危險操作必須確認**
```json
{
  "tools": {
    "reset-db": {
      "description": "重置資料庫（⚠️ 會刪除所有資料）",
      "command": "npm run db:reset",
      "confirm": true
    }
  }
}
```

3. **限制工具執行範圍**
```json
{
  "tools": {
    "cleanup": {
      "workingDir": "${workspaceFolder}/temp",
      "command": "rm -rf ./*"
    }
  }
}
```

## 🎮 使用自定義工具

### 🎯 **在對話中調用**

```bash
# 直接使用工具名稱
> 請使用 deploy-staging 工具部署應用

# AI 會執行
🔧 執行 deploy-staging...
📦 正在部署到測試環境...
✅ 部署成功！

# 組合使用
> 請先執行 lint 檢查，通過後再執行 test
```

### 🎯 **查看可用工具**

```bash
/tools
```

輸出：
```
🛠️ 可用工具：
• deploy         - 部署應用到生產環境
• test           - 執行所有測試
• lint           - 檢查程式碼風格
• db-migrate     - 執行資料庫遷移
• cleanup        - 清理專案暫存檔案
```

---

## 🚀 下一步學習

現在你已經掌握了 OpenCode 的自定義工具系統！

👉 **[繼續：進階功能 →](../advanced/index.md)**

---

<div align="center">
  <p><strong>🔧 工具高手等級解鎖！</strong></p>
  <p>💡 訣竅：將重複性工作封裝成工具，讓 AI 幫你自動化</p>
</div>
