# ⚙️ 配置詳解

> 掌握 OpenCode 的配置選項，打造完全個人化的 AI 開發環境！

## 📋 配置概覽

OpenCode 提供了豐富的配置選項，讓你打造最適合自己需求的 AI 開發環境。

### 🎯 **配置分類**

```
🎨 外觀配置      - 主題、字體、界面布局
⌨️ 操作配置      - 快捷鍵、編輯器、行為設定
🤖 模型配置      - LLM 提供商、模型選擇、參數調整
🛠️ 功能配置      - 工具權限、插件設定、擴展選項
🔐 安全配置      - 權限控制、隱私設定、安全邊界
```

---

## 🎨 外觀配置

### 🎯 **主題配置**

#### **內建主題**
```bash
# 查看可用主題
/themes

# 切換主題
/config set theme tokyonight      # 深色主題
/config set theme default         # 淺色主題
/config set theme catppuccin       # Catppuccin 主題
/config set theme gruvbox         # Gruvbox 主題
/config set theme matrix          # 黑客風格
/config set theme one-dark        # One Dark 主題
```

#### **主題詳細介紹**

**🌙 Tokyonight（推薦深色主題）**
- 適合長時間工作，護眼
- 專業的配色方案
- 優秀的語法高亮
- 適合各種程式語言

**☀️ Default（淺色主題）**
- 日間工作首選
- 清爽簡潔的界面
- 良好的可讀性
- 適合文檔編寫

**🎨 Catppuccin（流行主題）**
- 溫和的配色方案
- 現代化的視覺效果
- 豐富的顏色層次
- 深受歡迎的設計

#### **自定義主題**
```json
{
  "$schema": "https://opencode.ai/config.json",
  "theme": {
    "name": "my-custom-theme",
    "colors": {
      "background": "#1e1e1e",
      "foreground": "#d4d4d4",
      "primary": "#007acc",
      "secondary": "#6c757d",
      "success": "#28a745",
      "warning": "#ffc107",
      "error": "#dc3545",
      "info": "#17a2b8",
      
      // 語法高亮顏色
      "syntaxKeyword": "#569cd6",
      "syntaxString": "#ce9178",
      "syntaxComment": "#6a9955",
      "syntaxFunction": "#dcdcaa",
      "syntaxVariable": "#9cdcfe",
      "syntaxType": "#4ec9b0"
    }
  }
}
```

### 🔤 **字體配置**

#### **字體設置**
```bash
# 設定字體系列
/config set font_family "JetBrains Mono"
/config set font_family "Fira Code"
/config set font_family "Source Code Pro"
/config set font_family "Hack"

# 設定字體大小
/config set font_size 12      # 小字體
/config set font_size 14      # 標準字體（推薦）
/config set font_size 16      # 大字體
/config set font_size 18      # 超大字體
```

#### **字體美化設定**
```bash
# 字體粗細
/config set font_weight normal
/config set font_weight medium
/config set font_weight bold

# 字體間距
/config set letter_spacing 0.0
/config set letter_spacing 0.1
/config set letter_spacing 0.2

# 行高設定
/config set line_height 1.2    # 緊湊
/config set line_height 1.4    # 標準（推薦）
/config set line_height 1.6    # 寬鬆
```

### 📐 **界面布局**

#### **邊距和間距**
```bash
# 界面邊距
/config set margin 4
/config set margin 6
/config set margin 8

# 組件間距
/config set spacing 2
/config set spacing 4
/config set spacing 6

# 內容邊距
/config set padding 8
/config set padding 12
/config set padding 16
```

#### **顯示選項**
```bash
# 顯示/隱藏界面元素
/config set show_title_bar true
/config set show_status_bar true
/config set show_line_numbers true
/config set show_scrollbar true

# 界面透明度
/config set opacity 1.0     # 不透明
/config set opacity 0.9     # 輕微透明
/config set opacity 0.8     # 中等透明
```

---

## ⌨️ 操作配置

### 🎯 **快捷鍵配置**

#### **基本快捷鍵設定**
```bash
# 設定 Leader 鍵
/config set keybinds.leader "ctrl+x"
/config set keybinds.leader "alt+space"
/config set keybinds.leader "f1"

# 查看所有快捷鍵
/keybinds show

# 重置快捷鍵
/keybinds reset
/keybinds reset all
```

#### **自定義快捷鍵**
```bash
# 設定具體快捷鍵
/keybinds set "ctrl+p" "command list"
/keybinds set "ctrl+t" "/test"
/keybinds set "ctrl+b" "/build"
/keybinds set "ctrl+s" "/share"

# 複合快捷鍵
/keybinds set "ctrl+x,c" "/connect"
/keybinds set "ctrl+x,m" "/models"
/keybinds set "ctrl,x,h" "/help"
```

#### **常用快捷鍵組合**
```bash
# 效率提升組合
/keybinds set "alt+1" "model claude-3-haiku"      # 快速切換模型
/keybinds set "alt+2" "model claude-3-sonnet"    # 快速切換模型
/keybinds set "alt+3" "model claude-3-5-sonnet"  # 快速切換模型

# 會話管理組合
/keybinds set "f2" "session new"                 # 新建會話
/keybinds set "f3" "session list"                # 列出會話
/keybinds set "f4" "session switch"              # 切換會話

# 開發工具組合
/keybinds set "f5" "/test"                       # 運行測試
/keybinds set "f6" "/build"                      # 執行構建
/keybinds set "f7" "/analyze"                    # 分析代碼
```

### 🎨 **編輯器配置**

#### **輸入行為設定**
```bash
# 自動完成
/config set auto_complete true
/config set auto_complete false

# 自動縮進
/config set auto_indent true
/config set indent_size 2
/config set indent_size 4

# 智能建議
/config set smart_suggestions true
/config set suggestion_threshold 0.8
```

#### **行為調整**
```bash
# 滾動行為
/config set scroll_speed 3
/config set smooth_scrolling true
/config set scroll_offset 5

# 複製行為
/config set auto_copy_selection true
/config set copy_with_line_numbers false

# 歷史記錄
/config set history_size 1000
/config set history_search true
```

---

## 🤖 模型配置

### 🔗 **提供商配置**

#### **OpenAI 配置**
```bash
# 基本配置
/config set provider.openai.api_key "sk-..."
/config set provider.openai.base_url "https://api.openai.com/v1"
/config set provider.openai.organization "org-..."

# 高級配置
/config set provider.openai.timeout 30
/config set provider.openai.max_retries 3
/config set provider.openai.temperature 0.7
```

#### **Anthropic 配置**
```bash
# 基本配置
/config set provider.anthropic.api_key "sk-ant-..."
/config set provider.anthropic.base_url "https://api.anthropic.com"

# 高級配置
/config set provider.anthropic.timeout 60
/config set provider.anthropic.max_retries 5
/config set provider.anthropic.temperature 0.7
```

#### **OpenCode Zen 配置**
```bash
# 推薦配置
/config set provider.opencode.api_key "zen-..."
/config set provider.opencode.base_url "https://api.opencode.ai"

# 自動模型選擇
/config set provider.opencode.auto_model true
/config set provider.opencode.smart_routing true
```

### 🧠 **模型選擇和調整**

#### **模型參數配置**
```bash
# 全域模型設定
/config set default_model "anthropic/claude-sonnet-4-5"
/config set small_model "anthropic/claude-haiku-4-5"
/config set fast_model "anthropic/claude-haiku-4-5"

# 模型參數調整
/config set model.temperature 0.7    # 創意程度 (0-1)
/config set model.max_tokens 4096     # 最大輸出長度
/config set model.top_p 0.9          # 核心採樣
/config set model.frequency_penalty 0 # 頻率懲罰
/config set model.presence_penalty 0  # 存在懲罰
```

#### **模型性能優化**
```bash
# 響應時間優化
/config set model.stream true       # 串流輸出
/config set model.timeout 30        # 超時設定
/config set model.retry_on_timeout true

# 成本控制
/config set model.cost_limit 10.0   # 每日成本限制
/config set model.token_limit 100000 # 每日 Token 限制
```

### 🔄 **模型自動切換**

#### **智能模型選擇**
```bash
# 基於任務類型自動選擇
/config set auto_model_selection true
/config set model_mapping.code_generation "anthropic/claude-sonnet-4-5"
/config set model_mapping.simple_tasks "anthropic/claude-haiku-4-5"
/config set model_mapping.creative_writing "anthropic/claude-sonnet-4-5"

# 基於複雜度自動選擇
/config set complexity_threshold 0.8
/config set simple_model "anthropic/claude-haiku-4-5"
/config set complex_model "anthropic/claude-sonnet-4-5"
```

---

## 🛠️ 功能配置

### 🔧 **工具權限配置**

#### **基本權限設定**
```bash
# 工具權限控制
/config set tools.read true
/config set tools.write true
/config set tools.edit true
/config set tools.bash true
/config set tools.webfetch true
/config set tools.websearch true

# 工具模式設定
/config set tools.safe_mode true
/config set tools.confirm_dangerous true
```

#### **細粒度權限控制**
```bash
# Bash 命令權限
/config set permission.bash.allow "git *, npm *, python *, ls, pwd, cd"
/config set permission.bash.ask "docker *, sudo *, rm -rf *"
/config set permission.bash.deny "rm -rf / *, chmod 777 *"

# 檔案操作權限
/config set permission.file.allow "*.js, *.ts, *.jsx, *.tsx, *.json"
/config set permission.file.ask "*.config.*, package-lock.json"
/config set permission.file.deny "id_rsa, *.pem, *.key"

# 網路存取權限
/config set permission.web.allow "github.com, stackoverflow.com, docs.python.org"
/config set permission.web.ask "*.example.com, internal.*"
/config set permission.web.deny "*.*.local, 127.0.0.1"
```

### 🧩 **插件配置**

#### **插件管理**
```bash
# 查看已安裝插件
/plugins list

# 啟用/禁用插件
/plugins enable github-integration
/plugins disable code-formatter

# 插件配置
/config set plugin.github.auto_commit true
/config set plugin.github.pull_request_template true
```

#### **常用插件配置**
```bash
# Git 集成插件
/config set plugin.git.auto_stage true
/config set plugin.git.auto_commit_message "AI generated changes"
/config set plugin.git.branch_prefix "ai-"

# 代碼格式化插件
/config set plugin.formatter.auto_format true
/config set plugin.formatter.format_on_save true
/config set plugin.formatter.prettier_config true

# 性能監控插件
/config set plugin.monitor.enabled true
/config set plugin.monitor.track_response_time true
/config set plugin.monitor.track_token_usage true
```

---

## 🔐 安全配置

### 🛡️ **權限和安全設定**

#### **安全模式**
```bash
# 啟用安全模式
/config set security_mode true
/config set security_level high    # low, medium, high, strict

# 安全檢查
/config set security.scan_code true
/config set security.validate_inputs true
/config set security.log_suspicious true
```

#### **隱私保護**
```bash
# 數據隱私設定
/config set privacy.anonymous_usage true
/config set privacy.disable_telemetry false
/config set privacy.encrypt_logs true

# 敏感資料保護
/config set privacy.mask_secrets true
/config set privacy.exclude_patterns "*.key, *.pem, .env*"
```

### 🔑 **認證和安全**

#### **API 密鑰管理**
```bash
# 密鑰存儲方式
/config set auth.store_method "keychain"  # keychain, file, memory
/config set auth.encrypt_keys true
/config set auth.auto_refresh false

# 會話安全
/config set session.timeout 3600      # 1 小時
/config set session.encrypt true
/config set session.require_auth true
```

---

## 🎯 個人化配置範例

### 👨‍💻 **前端開發者配置**
```json
{
  "theme": "tokyonight",
  "font_family": "JetBrains Mono",
  "font_size": 14,
  "line_height": 1.4,
  "default_model": "anthropic/claude-sonnet-4-5",
  "auto_model_selection": true,
  "keybinds": {
    "leader": "alt+space",
    "custom": {
      "alt+1": "model claude-3-haiku",
      "alt+2": "model claude-3-sonnet",
      "ctrl+t": "/test",
      "ctrl+b": "/build"
    }
  },
  "plugins": [
    "github-integration",
    "code-formatter",
    "eslint-integration"
  ],
  "permission": {
    "bash": {
      "allow": "npm *, yarn *, git *, node *"
    }
  }
}
```

### 🏗️ **後端開發者配置**
```json
{
  "theme": "default",
  "font_family": "Fira Code",
  "font_size": 13,
  "default_model": "anthropic/claude-3-5-sonnet",
  "model": {
    "temperature": 0.3,
    "max_tokens": 8192
  },
  "tools": {
    "bash": true,
    "websearch": true
  },
  "permission": {
    "bash": {
      "allow": "docker *, python *, pip *, git *, npm *",
      "ask": "sudo *, systemctl *"
    }
  }
}
```

### 🔒 **企業環境配置**
```json
{
  "theme": "default",
  "font_size": 12,
  "security_mode": true,
  "security_level": "strict",
  "privacy": {
    "anonymous_usage": true,
    "disable_telemetry": true,
    "encrypt_logs": true
  },
  "auth": {
    "store_method": "keychain",
    "encrypt_keys": true,
    "session": {
      "timeout": 1800,
      "require_auth": true
    }
  },
  "permission": {
    "web": {
      "allow": "*.company.com, github.com",
      "deny": "*"
    },
    "bash": {
      "allow": "git *, npm *, python *",
      "deny": "sudo *, rm -rf *"
    }
  }
}
```

---

## 🔧 配置管理

### 📁 **配置檔案位置**

#### **標準配置路徑**
```bash
# 全域配置
~/.config/opencode/opencode.json
~/.config/opencode/themes/
~/.config/opencode/keybinds.json

# 專案配置
./opencode.json
./.opencode/
./AGENTS.md

# 環境變數覆蓋
OPENCODE_CONFIG="/path/to/custom/config.json"
OPENCODE_CONFIG_DIR="/path/to/config/directory"
```

#### **配置檔案管理**
```bash
# 導出配置
/config export --full my-backup.json
/config export --theme themes-backup.json
/config export --keybinds keybinds-backup.json

# 導入配置
/config import my-backup.json
/config import --themes themes-backup.json

# 重置配置
/config reset
/config reset --theme
/config reset --keybinds
```

### 🔄 **配置同步**

#### **多設備同步**
```bash
# 啟用配置同步
/config set sync.enabled true
/config set sync.provider "github"  # github, dropbox, custom
/config set sync.github.repo "username/opencode-config"

# 同步配置
/sync upload
/sync download
/sync status
```

---

## 🎉 配置最佳實踐

### ✅ **配置原則**

1. **漸進式配置** - 從基本配置開始，逐步調整
2. **場景化配置** - 為不同工作場景創建配置檔案
3. **版本控制** - 將配置檔案納入版本控制
4. **定期備份** - 定期備份重要配置
5. **團隊統一** - 團隊成員使用統一的基礎配置

### 🎯 **實施建議**

1. **從預設開始** - 先熟悉預設配置
2. **記錄變更** - 記錄每次配置變更的原因
3. **測試效果** - 配置變更後充分測試
4. **分享經驗** - 將好的配置分享給團隊

---

## 🚀 下一步學習

現在 你已經完全掌握了 OpenCode 的配置系統！

👉 **[繼續：進階功能 →](../advanced/skills-system.md)**

---

<div align="center">
  <p><strong>恭喜！你已經成為 OpenCode 配置的專家！</strong></p>
  <p>💡 訣竅：找到最適合自己的配置，讓工具真正為你服務</p>
</div>