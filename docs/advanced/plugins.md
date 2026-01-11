# 🧩 插件開發

> 創建自己的 OpenCode 插件，擴展 AI 助手的無限可能！

## 🎯 插件系統概覽

OpenCode 的插件系統允許開發者創建自定義功能，為 AI 助手增加新的能力。插件可以新增命令、工具、代理、主題等各種擴展。

### 🏗️ **插件類型**

```
🧩 插件類別
├── 命令插件      (新增 /commands)
├── 工具插件      (新增 AI 可調用的工具)
├── 代理插件      (新增自定義代理)
├── 主題插件      (自定義界面主題)
├── 整合插件      (第三方服務整合)
└── 語言插件      (程式語言支援)
```

## 📦 插件結構

### 🎯 **基本目錄結構**

```
my-opencode-plugin/
├── package.json          # 插件元數據
├── src/
│   ├── index.ts          # 插件入口點
│   ├── commands/         # 命令定義
│   ├── tools/            # 工具定義
│   └── agents/           # 代理定義
├── assets/
│   └── icon.png          # 插件圖標
└── README.md             # 插件文檔
```

### 🎯 **package.json 配置**

```json
{
  "name": "opencode-plugin-example",
  "version": "1.0.0",
  "description": "我的 OpenCode 插件",
  "main": "dist/index.js",
  "opencode": {
    "type": "plugin",
    "displayName": "範例插件",
    "description": "這是一個範例插件",
    "category": "utilities",
    "activationEvents": [
      "onCommand:example.hello",
      "onStartup"
    ]
  },
  "devDependencies": {
    "@opencode/sdk": "^1.0.0",
    "typescript": "^5.0.0"
  }
}
```

## ⌨️ 開發命令插件

### 🎯 **基本命令**

```typescript
// src/commands/hello.ts
import { OpenCodePlugin, Command } from "@opencode/sdk";

export const helloCommand: Command = {
  name: "hello",
  description: "打招呼的範例命令",
  usage: "/hello [name]",
  
  async execute(context, args) {
    const name = args[0] || "世界";
    
    await context.reply(`👋 你好，${name}！`);
  }
};
```

### 🎯 **帶參數的命令**

```typescript
// src/commands/search.ts
import { Command, CommandContext } from "@opencode/sdk";

export const searchCommand: Command = {
  name: "search",
  description: "搜尋專案中的程式碼",
  usage: "/search <pattern> [--type <type>]",
  options: [
    {
      name: "type",
      alias: "t",
      description: "檔案類型過濾",
      type: "string"
    }
  ],
  
  async execute(context: CommandContext, args: string[], options: Record<string, any>) {
    const pattern = args[0];
    const fileType = options.type;
    
    if (!pattern) {
      return context.error("請提供搜尋模式");
    }
    
    const results = await context.workspace.search(pattern, {
      fileType: fileType
    });
    
    await context.reply(`找到 ${results.length} 個結果`);
    
    for (const result of results.slice(0, 10)) {
      await context.reply(`📄 ${result.file}:${result.line}`);
    }
  }
};
```

## 🔧 開發工具插件

### 🎯 **基本工具**

```typescript
// src/tools/weather.ts
import { Tool, ToolContext } from "@opencode/sdk";

export const weatherTool: Tool = {
  name: "get_weather",
  description: "取得指定城市的天氣資訊",
  inputSchema: {
    type: "object",
    properties: {
      city: {
        type: "string",
        description: "城市名稱"
      },
      units: {
        type: "string",
        enum: ["celsius", "fahrenheit"],
        default: "celsius"
      }
    },
    required: ["city"]
  },
  
  async execute(context: ToolContext, input: { city: string; units?: string }) {
    const { city, units = "celsius" } = input;
    
    // 呼叫天氣 API
    const weather = await fetchWeather(city);
    
    return {
      city: city,
      temperature: weather.temp,
      units: units,
      condition: weather.condition,
      humidity: weather.humidity
    };
  }
};
```

### 🎯 **資料庫工具**

```typescript
// src/tools/database.ts
import { Tool } from "@opencode/sdk";

export const queryTool: Tool = {
  name: "query_database",
  description: "執行資料庫查詢",
  inputSchema: {
    type: "object",
    properties: {
      query: { type: "string", description: "SQL 查詢語句" },
      database: { type: "string", description: "資料庫名稱" }
    },
    required: ["query"]
  },
  
  // 標記為危險操作，需要用戶確認
  dangerous: true,
  
  async execute(context, input) {
    const { query, database } = input;
    
    const connection = await context.getDatabase(database);
    const results = await connection.query(query);
    
    return {
      rowCount: results.length,
      rows: results
    };
  }
};
```

## 🤖 開發代理插件

### 🎯 **自定義代理**

```typescript
// src/agents/security-expert.ts
import { Agent, AgentContext } from "@opencode/sdk";

export const securityExpert: Agent = {
  name: "security-expert",
  displayName: "資訊安全專家",
  description: "專注於代碼安全審查和漏洞檢測",
  
  systemPrompt: `你是一位資訊安全專家，專注於：
- 代碼安全審查
- 漏洞檢測和分析
- 安全最佳實踐建議
- OWASP 十大風險分析

請以安全的角度分析所有代碼和配置。`,
  
  model: "anthropic/claude-sonnet-4-5",
  temperature: 0.2,
  
  tools: ["read", "websearch"],
  
  async onActivate(context: AgentContext) {
    console.log("安全專家代理已啟動");
  }
};
```

## 🎨 開發主題插件

### 🎯 **自定義主題**

```typescript
// src/themes/dracula.ts
import { Theme } from "@opencode/sdk";

export const draculaTheme: Theme = {
  name: "dracula",
  displayName: "Dracula 暗色主題",
  type: "dark",
  
  colors: {
    background: "#282a36",
    foreground: "#f8f8f2",
    primary: "#bd93f9",
    secondary: "#6272a4",
    accent: "#ff79c6",
    error: "#ff5555",
    warning: "#f1fa8c",
    success: "#50fa7b",
    info: "#8be9fd"
  },
  
  syntax: {
    keyword: "#ff79c6",
    string: "#f1fa8c",
    comment: "#6272a4",
    function: "#50fa7b",
    variable: "#8be9fd",
    number: "#bd93f9"
  }
};
```

## 📦 插件發佈

### 🎯 **發佈到 npm**

```bash
# 建置插件
npm run build

# 登入 npm
npm login

# 發佈
npm publish
```

### 🎯 **發佈到 OpenCode 插件市場**

```bash
# 安裝發佈工具
npm install -g @opencode/cli

# 驗證插件
opencode plugin validate

# 發佈到市場
opencode plugin publish
```

## 🔧 除錯和測試

### 🎯 **本地開發**

```bash
# 啟用開發模式
npm run dev

# 連接到 OpenCode
opencode --plugin-dev ./dist
```

### 🎯 **單元測試**

```typescript
// tests/commands.test.ts
import { describe, it, expect } from "vitest";
import { helloCommand } from "../src/commands/hello";

describe("Hello Command", () => {
  it("should greet with default name", async () => {
    const mockContext = createMockContext();
    await helloCommand.execute(mockContext, []);
    
    expect(mockContext.replies[0]).toContain("世界");
  });
  
  it("should greet with custom name", async () => {
    const mockContext = createMockContext();
    await helloCommand.execute(mockContext, ["OpenCode"]);
    
    expect(mockContext.replies[0]).toContain("OpenCode");
  });
});
```

## 📚 API 參考

### 🎯 **Context API**

```typescript
interface PluginContext {
  // 工作區操作
  workspace: {
    readFile(path: string): Promise<string>;
    writeFile(path: string, content: string): Promise<void>;
    search(pattern: string): Promise<SearchResult[]>;
  };
  
  // 用戶互動
  reply(message: string): Promise<void>;
  error(message: string): Promise<void>;
  confirm(message: string): Promise<boolean>;
  
  // 配置存取
  config: {
    get(key: string): any;
    set(key: string, value: any): Promise<void>;
  };
}
```

---

## 🚀 下一步學習

現在你已經掌握了 OpenCode 插件開發！

👉 **[繼續：企業部署 →](enterprise.md)**

---

<div align="center">
  <p><strong>🧩 插件開發者等級解鎖！</strong></p>
  <p>💡 訣竅：從簡單的命令插件開始，逐步擴展功能</p>
</div>
