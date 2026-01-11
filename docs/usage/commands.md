# ⚡ 命令詳解

> OpenCode 完整命令參考手冊，掌握每個命令的細微差別和進階用法！

## 📋 命令總覽

OpenCode 提供了豐富的命令系統，分為三大類別：

### 🎯 **命令分類**
```
🚀 啟動命令      - 控制程式的啟動和配置
🔧 系統命令      - 核心功能和狀態管理  
🛠️ 開發命令      - 開發相關的專門功能
```

---

## 🚀 啟動命令

### 📝 **opencode** - 主命令

#### **基本語法**
```bash
opencode [options] [message]
```

#### **常用選項**
| 選項 | 簡寫 | 描述 | 預設值 |
|------|------|------|--------|
| `--help` | `-h` | 顯示幫助資訊 | false |
| `--version` | `-v` | 顯示版本資訊 | false |
| `--model` | `-m` | 指定 AI 模型 | 預設模型 |
| `--session` | `-s` | 指定會話 ID | default |
| `--continue` | `-c` | 繼續上次會話 | false |
| `--debug` | `-d` | 啟用調試模式 | false |

#### **實際使用範例**
```bash
# 基本啟動
opencode

# 指定模型啟動
opencode --model anthropic/claude-sonnet-4-5

# 繼續上次會話
opencode --continue

# 指定會話名稱
opencode --session my-project

# 調試模式啟動
opencode --debug

# 複合選項
opencode --model claude-3-haiku --session web-dev --debug
```

### 🏃 **opencode run** - 非互動模式

#### **基本語法**
```bash
opencode run [options] <message>
```

#### **專用選項**
| 選項 | 簡寫 | 描述 | 範例 |
|------|------|------|------|
| `--attach` | `-a` | 連接到運行中的服務器 | `--attach http://localhost:4096` |
| `--output` | `-o` | 指定輸出格式 | `--output json` |
| `--file` | `-f` | 從檔案讀取輸入 | `--file input.txt` |

#### **實際使用範例**
```bash
# 基本非互動執行
opencode run "請用 Python 創建一個 Hello World 程式"

# 從檔案讀取並執行
opencode run --file task.txt

# 連接到遠程服務器執行
opencode run --attach http://localhost:4096 "分析這個 API"

# 指定輸出格式
opencode run --output json "解釋什麼是 REST API"

# 管道輸入
echo "檢查這個程式碼" | opencode run
```

### 🌐 **opencode serve** - 啟動服務器

#### **基本語法**
```bash
opencode serve [options]
```

#### **服務器選項**
| 選項 | 描述 | 預設值 |
|------|------|--------|
| `--port` | 指定服務器端口 | 4096 |
| `--host` | 指定綁定地址 | 0.0.0.0 |
| `--cors` | 啟用 CORS | true |
| `--auth` | 啟用認證 | false |

#### **實際使用範例**
```bash
# 啟動預設服務器
opencode serve

# 指定端口
opencode serve --port 8080

# 本地綁定
opencode serve --host 127.0.0.1

# 啟用認證
opencode serve --auth

# 完整配置
opencode serve --port 8080 --host 0.0.0.0 --cors --auth
```

---

## 🔧 系統命令

### 🔗 **連接管理**

#### **/connect** - 連接提供商
```bash
# TUI 中的使用
/connect

# 連接後的互動流程
1. 選擇提供商 (opencode, openai, anthropic, etc.)
2. 輸入 API 金鑰或完成 OAuth 認證
3. 測試連接並確認
```

#### **/auth** - 認證管理
```bash
# 查看已認證的提供商
/auth list

# 登入新提供商
/auth login

# 登出特定提供商
/auth logout openai

# 重新認證
/auth reauth anthropic
```

#### **/models** - 模型管理
```bash
# 顯示所有可用模型
/models

# 刷新模型快取
/models --refresh

# 顯示模型詳細資訊
/models --detailed

# 過濾特定類型模型
/models --type chat
/models --provider openai
```

### 📊 **會話管理**

#### **/session** - 會話操作
```bash
# 查看所有會話
/session list

# 創建新會話
/session new web-project

# 切換會話
/session switch api-development

# 刪除會話
/session delete old-session

# 導出會話
/session export --format json
/session export --format markdown

# 檢查會話統計
/session stats web-project
```

#### **/history** - 歷史管理
```bash
# 顯示對話歷史
/history

# 清空歷史
/history clear

# 搜索歷史
/history search "REST API"

# 顯示歷史統計
/history stats

# 導出歷史
/history export history.md
```

### ⚙️ **配置管理**

#### **/config** - 配置操作
```bash
# 顯示所有配置
/config show

# 顯示特定配置
/config show theme
/config show model

# 設定配置
/config set theme tokyonight
/config set default_model anthropic/claude-haiku
/config set share auto

# 重置配置
/config reset
/config reset theme

# 導入配置
/config import config.json

# 導出配置
/config export backup.json
```

#### **/keybinds** - 快捷鍵管理
```bash
# 顯示快捷鍵綁定
/keybinds show

# 設定快捷鍵
/keybinds set <key> <command>
/keybinds set ctrl+p "command list"

# 重置快捷鍵
/keybinds reset
/keybinds reset ctrl+p

# 導出快捷鍵配置
/keybinds export my-keybinds.json
```

---

## 🛠️ 開發命令

### 📁 **檔案操作**

#### **檔案引用**
```bash
# 引用單一檔案
@package.json
> 請分析 @package.json 的依賴關係

# 引用目錄
@src/
> 請總結 @src/ 目錄中的所有元件

# 模糊搜索檔案
@config
> 請檢查 @config 中的所有配置檔案

# 絕對路徑引用
@/etc/hosts
> 請檢查 /etc/hosts 檔案
```

#### **檔案操作命令**
```bash
# 讀取檔案
/read <filename>
/read src/main.js

# 列出目錄內容
/list
/list src/
/list --detailed

# 創建檔案
/create <filename> <content>
/create utils.js "export const helper = () => {}"

# 複製檔案
/copy <source> <destination>
/copy src/app.js src/app.backup.js

# 移動/重命名檔案
/move <source> <destination>
/move old-name.js new-name.js
```

### 🔍 **搜索和分析**

#### **/search** - 內容搜索
```bash
# 搜索檔案內容
/search "function handleClick"
/search --pattern "async.*await"

# 搜索檔名
/search --filename "test"
/search --filename "*.spec.js"

# 上下文搜索
/search --context 3 "error handling"
/search --before 2 --after 2 "try"

# 正則表達式搜索
/search --regex "const\s+\w+\s*=\s*async"
```

#### **/analyze** - 代碼分析
```bash
# 分析單一檔案
/analyze src/main.js

# 分析目錄
/analyze src/components/

# 指定分析類型
/analyze --type complexity src/
/analyze --type security src/api/
/analyze --type performance src/utils/

# 生成分析報告
/analyze --report analysis-report.html
/analyze --format json src/
```

### 🧪 **測試和構建**

#### **/test** - 測試管理
```bash
# 運行所有測試
/test

# 運行特定測試
/test unit
/test integration
/test e2e

# 運行特定檔案的測試
/test src/components/Button.test.js

# 測試覆蓋率
/test --coverage
/test --coverage --format lcov

# 監視模式測試
/test --watch
```

#### **/build** - 構建管理
```bash
# 運行構建
/build

# 指定構建目標
/build production
/build development
/build staging

# 清理構建
/build clean

# 增量構建
/build --incremental

# 構建分析
/build --analyze
/build --stats
```

---

## 🔧 高級命令組合

### 🎯 **命令管道**

#### **基本管道操作**
```bash
# 串聯命令
> 請分析 @src/main.js | 請總結發現的問題
> 請搜索所有測試檔案 | 請檢查測試覆蓋率

# 條件管道
> 請檢查程式碼風格 && 請自動修復問題
> 請測試構建 || 請分析失敗原因
```

#### **複雜管道**
```bash
# 多步驟處理管道
> 請搜索所有 API 端點 | 
  請檢查安全性 | 
  請生成安全報告 | 
  請創建修復建議

# 條件分支管道
> 請檢查套件更新 ?
  (請更新所有套件) :
  (請顯示可用的更新)
```

### 🎨 **命令宏**

#### **創建命令宏**
```bash
# 定義簡單宏
/macro create setup-project
> 請初始化 npm 專案
> 請創建基本目錄結構
> 請設定 Git 倉庫
> 請安裝開發依賴

# 定義參數化宏
/macro create create-component <name>
> 請在 src/components/ 創建 <name> 元件
> 請為 <name> 元件撰寫測試
> 請更新元件索引檔案
```

#### **使用命令宏**
```bash
# 執行宏
/macro run setup-project

# 使用參數執行宏
/macro run create-component UserCard
/macro run create-component NavigationBar
```

### ⚡ **批量操作**

#### **批量檔案處理**
```bash
# 批量重命名
/batch rename --pattern "*.js" --to "*.ts"

# 批量格式化
/batch format --ext .js,.ts,.jsx,.tsx

# 批量搜尋替換
/batch replace --from "var" --to "const" --ext .js

# 批量分析
/batch analyze --type complexity --ext .js
```

---

## 🔍 調試和診斷

### 🩺 **系統診斷**

#### **/doctor** - 全面診斷
```bash
# 完整系統診斷
/doctor

# 特定項目診斷
/doctor network
/doctor filesystem
/doctor permissions
/doctor configuration

# 生成診斷報告
/doctor --report system-health.json
/doctor --detailed
```

#### **/logs** - 日誌管理
```bash
# 顯示日誌
/logs
/logs --tail 50

# 過濾日誌
/logs --level error
/logs --since "2024-01-01"

# 導出日誌
/logs export logs.txt
/logs export --format json
```

#### **/debug** - 調試模式
```bash
# 啟用調試模式
/debug

# 設定調試級別
/debug verbose
/debug minimal

# 調試特定功能
/debug network
/debug api
/debug filesystem
```

### 📊 **性能監控**

#### **/monitor** - 性能監控
```bash
# 開始監控
/monitor start

# 查看監控狀態
/monitor status

# 停止監控
/monitor stop

# 導出監控數據
/monitor export performance.json
```

#### **/profile** - 性能分析
```bash
# 開始性能分析
/profile start

# 分析特定操作
/profile analyze "command execution"
/profile analyze "file operations"

# 生成分析報告
/profile report
/profile export profile-data.json
```

---

## 🎨 自定義命令

### 🔧 **創建自定義命令**

#### **方法一：互動式創建**
```bash
# 開始創建命令
/command create

# 互動式對話：
> 請輸入命令名稱: test-all
> 請輸入命令描述: 運行所有類型的測試並生成報告
> 請輸入命令模板: npm test && npm run test:coverage && npm run test:e2e
> 請選擇執行代理: build
```

#### **方法二：檔案創建**
```bash
# 創建命令檔案
touch .opencode/command/test-all.md

# 編輯命令內容
---
description: 運行所有類型的測試並生成報告
agent: build
template: |
  npm test && npm run test:coverage && npm run test:e2e
---
```

### 🎯 **高級自定義命令**

#### **參數化命令**
```bash
# .opencode/command/create-api.md
---
description: 創建 REST API 端點
template: |
  請在 src/api/ 創建 ${endpoint}.js
  包含以下方法：${methods}
  使用資料庫模型：${model}
  實現錯誤處理和輸入驗證
---

# 使用方式
/create-api --endpoint users --methods "GET,POST,PUT,DELETE" --model User
```

#### **條件命令**
```bash
# .opencode/command/deploy-check.md
---
description: 部署前檢查
template: |
  請執行部署前檢查：
  ${TESTS:+運行測試套件}
  ${LINT:+檢查程式碼風格}
  ${BUILD:+執行構建}
  ${SECURITY:+進行安全掃描}
---

# 使用方式
/deploy-check TESTS=1 LINT=1 BUILD=1
```

---

## 📚 命令參考速查表

### 🚀 **快速命令參考**

| 類別 | 命令 | 功能 | 範例 |
|------|------|------|------|
| **啟動** | `opencode` | 啟動 TUI | `opencode --model claude-3-haiku` |
| | `opencode run` | 非互動執行 | `opencode run "Hello World"` |
| | `opencode serve` | 啟動服務器 | `opencode serve --port 8080` |
| **連接** | `/connect` | 連接提供商 | `/connect` |
| | `/auth` | 認證管理 | `/auth list` |
| | `/models` | 模型管理 | `/models --refresh` |
| **檔案** | `@file` | 檔案引用 | `@package.json` |
| | `/read` | 讀取檔案 | `/read src/main.js` |
| | `/search` | 搜索內容 | `/search "function"` |
| **系統** | `/config` | 配置管理 | `/config set theme dark` |
| | `/session` | 會話管理 | `/session new project` |
| | `/help` | 顯示幫助 | `/help` |

### 🔧 **進階命令組合**

| 組合 | 功能 | 範例 |
|------|------|------|
| **分析管道** | 深度代碼分析 | `@src/ | /analyze security | /generate report` |
| **批量處理** | 多檔案操作 | `/batch format --ext .js,.ts` |
| **測試構建** | 完整驗證流程 | `/test && /build && /analyze` |
| **部署檢查** | 部署前驗證 | `/lint && /test && /security-scan` |

---

## 🔧 故障排除

### ❌ **常見命令錯誤**

#### **模型錯誤**
```bash
# 問題：模型不可用
> /model gpt-5
❌ Error: Model 'gpt-5' not available

# 解決方案
/models --refresh
/model claude-3-haiku
```

#### **檔案權限錯誤**
```bash
# 問題：無法訪問檔案
> /etc/hosts
❌ Error: Permission denied

# 解決方案
/sudo read /etc/hosts
# 或
/config set safe_mode false
```

#### **網路連接錯誤**
```bash
# 問題：無法連接提供商
> /connect openai
❌ Error: Network timeout

# 解決方案
/doctor network
/config set timeout 30
```

### 🛠️ **調試技巧**

#### **詳細錯誤資訊**
```bash
# 啟用詳細日誌
/debug verbose

# 檢查系統狀態
/doctor --detailed

# 查看完整錯誤堆疊
/logs --trace
```

#### **命令執行追蹤**
```bash
# 追蹤命令執行
/trace command /models

# 追蹤檔案操作
/trace file @package.json

# 追蹤網路請求
/trace network /connect
```

---

## 🎉 最佳實踐總結

### ✅ **高效使用原則**

1. **善用檔案引用** - `@file` 符號是最強大的功能
2. **組合命令使用** - 管道和批量操作提升效率
3. **自定義常用操作** - 創建個人化的命令快捷方式
4. **定期維護會話** - 清理舊會話保持系統輕量

### 🎯 **進階技巧**

1. **命令腳本化** - 將重複性操作轉化為可重用腳本
2. **性能監控** - 使用監控命令優化使用效率
3. **錯誤預防** - 使用診斷命令提前發現問題
4. **自動化整合** - 與其他開發工具無縫整合

---

## 🚀 下一步學習

現在 你已經完全掌握了 OpenCode 的所有命令！

👉 **[繼續：最佳實踐指南 →](best-practices.md)**

---

<div align="center">
  <p><strong>恭喜！你已經成為 OpenCode 命令的專家！</strong></p>
  <p>💡 訣竅：熟能生巧，多練習，形成個人的高效工作流程</p>
</div>