# ⚡ 基本命令

> 掌握 OpenCode 的核心命令，讓你如虎添翼！這裡是日常使用最重要的命令速查表。

## 📋 命令分類導覽

OpenCode 的命令分為三大類：

### 🎯 **核心命令** - 必掌握的日常操作
### 🔧 **進階命令** - 提升效率的專業功能  
### 🎨 **管理命令** - 系統和會話管理

---

## 🎯 核心命令（必掌握）

### 🚀 **啟動和基本操作**

| 命令 | 簡寫 | 功能描述 | 使用範例 |
|------|------|----------|----------|
| `opencode` | `oc` | 啟動 TUI 界面 | `opencode` |
| `opencode run <msg>` | `ocr` | 非互動模式執行 | `opencode run "Hello"` |
| `opencode --help` | `och` | 顯示幫助資訊 | `opencode --help` |
| `opencode --version` | `ocv` | 顯示版本資訊 | `opencode --version` |

#### 🔧 **實際使用範例**

```bash
# 基本啟動
opencode

# 指定模型啟動
opencode --model anthropic/claude-sonnet-4-5

# 繼續上次的會話
opencode --continue

# 直接執行單次任務
opencode run "請用 Python 創建一個 Hello World 程式"

# 查看版本
opencode --version
# 輸出: opencode version 1.0.0
```

### 🔑 **連接和認證**

| 命令 | 功能描述 | 使用注意事項 |
|------|----------|--------------|
| `/connect` | 連接 LLM 提供商 | 支援 75+ 提供商 |
| `/auth login` | 登入提供商帳戶 | 某些提供商需瀏覽器認證 |
| `/auth list` | 查看已認證提供商 | 顯示所有已連接的服務 |
| `/auth logout <provider>` | 登出特定提供商 | 需要提供商名稱 |

#### 🎯 **實際操作流程**

```bash
# 1. 連接提供商（在 TUI 中）
/connect

# 2. 選擇提供商（例如：opencode）
# 使用方向鍵選擇，Enter 確認

# 3. 輸入 API 金鑰
# 在瀏覽器獲取金鑰，貼上到終端

# 4. 驗證連接
> 請用繁體中文說「連接成功」

# 5. 查看認證狀態
/auth list
```

### 📊 **模型管理**

| 命令 | 功能描述 | 輸出格式 |
|------|----------|----------|
| `/models` | 顯示可用模型列表 | 表格格式，包含類型、上下文長度 |
| `/models --refresh` | 刷新模型快取 | 重新獲取最新模型資訊 |
| `/model <model-name>` | 切換到指定模型 | 即時生效 |

#### 🎨 **模型選擇策略**

```bash
# 查看所有可用模型
/models

# 典型輸出：
┌─────────────────────────────┬──────────┬─────────────┬────────────┐
│ Model                      │ Type     │ Context     │ Cost/1K    │
├─────────────────────────────┼──────────┼─────────────┼────────────┤
│ claude-3-5-sonnet          │ Anthropic│ 200K        │ $0.015     │
│ claude-3-haiku             │ Anthropic│ 200K        │ $0.0025    │
│ gpt-4o                     │ OpenAI   │ 128K        │ $0.005     │
│ gpt-4o-mini                │ OpenAI   │ 128K        │ $0.00015   │
└─────────────────────────────┴──────────┴─────────────┴────────────┘

# 切換到經濟實惠的模型
/model claude-3-haiku

# 切換到高品質模型（用於重要任務）
/model claude-3-5-sonnet
```

### 🎯 **檔案操作和引用**

| 符號/命令 | 功能描述 | 使用技巧 |
|----------|----------|----------|
| `@filename` | 引用特定檔案 | 支援模糊搜索 |
| `@dirname/` | 引用目錄內所有檔案 | 適用於整體分析 |
| `/read <file>` | 讀取檔案內容 | 等同於 @file |
| `/list` | 顯示當前目錄檔案 | 快速檢視專案結構 |

#### 🎨 **檔案引用實戰**

```bash
# 引用單一檔案
> 請分析 @package.json 的依賴關係

# 引用特定檔案（支援模糊搜索）
> 解釋 @src/utils/helper.ts 中的函數

# 引用整個目錄
> 請總結 @src/components/ 目錄中所有元件的功能

# 讀取檔案（替代方式）
> /read README.md
> 請為這個專案撰寫 100 字摘要
```

### 🔄 **模式切換和控制**

| 命令/快捷鍵 | 功能描述 | 應用場景 |
|-------------|----------|----------|
| `Tab` | 切換 Build/Plan 模式 | 安全規劃 vs 實際執行 |
| `/undo` | 撤銷上一次操作 | 錯誤修正 |
| `/redo` | 重做已撤銷的操作 | 恢復正確的修改 |
| `/clear` | 清空對話歷史 | 重新開始新主題 |

#### 🎯 **模式切換實戰**

```bash
# 在 Build Mode 中（預設）
> 請創建一個 Python 腳本，實現資料備份功能
# AI 會直接創建檔案並執行

# 切換到 Plan Mode
<Tab>

# 現在在 Plan Mode 中
> 請創建一個 Python 腳本，實現資料備份功能
# AI 會提供詳細計劃，但不執行

# 切換回 Build Mode
<Tab>

# 撤銷上一次操作
/undo

# 重做被撤銷的操作
/redo
```

---

## 🔧 進階命令（效率提升）

### 📤 **分享和協作**

| 命令 | 功能描述 | 使用場景 |
|------|----------|----------|
| `/share` | 分享當前會話 | 團隊協作、問題求助 |
| `/share --public` | 公開分享會話 | 社群展示、教學 |
| `/unshare` | 取消分享 | 隱私保護 |
| `/export <format>` | 匯出會話資料 | 本地保存、分析 |

#### 🎨 **分享功能實戰**

```bash
# 分享當前會話
/share
# 輸出: 🔗 分享連結已複製到剪貼簿: https://opencode.ai/s/abc123def456

# 公開分享（可被搜尋引擎收錄）
/share --public

# 匯出會話為 JSON
/export json
# 匯出會話為 Markdown
/export markdown

# 取消所有分享
/unshare
```

### 🧠 **智能代理調用**

| 命令 | 功能描述 | 使用技巧 |
|------|----------|----------|
| `@agent <name>` | 調用特定子代理 | 利用專家代理的專業能力 |
| `/agent list` | 顯示可用代理列表 | 查看所有專業代理 |
| `/agent create <name>` | 創建新代理 | 自定義專業行為 |

#### 🎯 **代理調用實戰**

```bash
# 查看可用代理
/agent list
# 輸出:
# - build: 主代理，完整功能
# - plan: 規劃代理，分析專精
# - general: 通用代理，研究專精
# - explore: 探索代理，快速搜索

# 調用通用代理進行研究
@general 請研究 React 19 的新功能，並提供詳細說明

# 調用探索代理快速搜索
@explore 找出專案中所有的 API 端點定義

# 調用代理進行程式碼審查
@agent code-reviewer 請審查 @src/main.js 的程式碼品質
```

### 🎨 **自定義命令**

| 命令 | 功能描述 | 創建方式 |
|------|----------|----------|
| `/<custom>` | 執行自定義命令 | 通过 `.opencode/command/` 目錄 |
| `/command list` | 顯示自定義命令 | 查看所有可用命令 |
| `/command create <name>` | 創建新命令 | 互動式命令建立 |

#### 🎯 **自定義命令實戰**

```bash
# 查看自定義命令
/command list

# 創建一個常用命令
/command create test
# 輸入命令描述: "執行完整的測試套件"
# 輸入命令模板: "npm test && npm run test:coverage"

# 使用自定義命令
/test
# AI 會執行: npm test && npm run test:coverage
```

### 📊 **會話和狀態管理**

| 命令 | 功能描述 | 使用場景 |
|------|----------|----------|
| `/session list` | 顯示所有會話 | 管理多個專案會話 |
| `/session new <name>` | 創建新會話 | 隔離不同專案 |
| `/session switch <name>` | 切換會話 | 在專案間快速切換 |
| `/stats` | 顯示使用統計 | 了解使用習慣 |

#### 🎯 **會話管理實戰**

```bash
# 查看所有會話
/session list
# 輸出:
# - default: 當前會話
# - web-project: Web 開發專案
# - api-project: API 開發專案

# 創建新會話
/session new python-ml

# 切換會話
/session switch web-project

# 查看使用統計
/stats
# 顯示: 使用時長、 token 消耗、常用模型等
```

---

## 🎨 管理命令（系統控制）

### ⚙️ **配置管理**

| 命令 | 功能描述 | 設定檔位置 |
|------|----------|------------|
| `/config show` | 顯示當前配置 | `~/.config/opencode/opencode.json` |
| `/config set <key> <value>` | 設定配置項 | 即時生效 |
| `/config reset` | 重置為預設配置 | 會清除所有自定義設定 |

#### 🔧 **配置管理實戰**

```bash
# 查看當前配置
/config show

# 設定預設模型
/config set default_model anthropic/claude-haiku

# 設定主題
/config set theme tokyonight

# 設定分享模式
/config set share manual

# 重置配置
/config reset
```

### 🔍 **調試和診斷**

| 命令 | 功能描述 | 用於問題解決 |
|------|----------|--------------|
| `/logs` | 顯示日誌資訊 | 系統問題診斷 |
| `/debug` | 進入調試模式 | 詳細的操作追蹤 |
| `/health` | 系統健康檢查 | 確保一切正常 |
| `/doctor` | 系統診斷工具 | 全面問題檢測 |

#### 🎯 **診斷命令實戰**

```bash
# 系統健康檢查
/health
# 輸出: ✅ 所有系統正常運行

# 查看日誌
/logs
# 顯示最近的操作日誌和錯誤資訊

# 系統診斷
/doctor
# 檢查: 網路連接、API 金鑰、檔案權限等
```

### 🚀 **系統控制**

| 命令 | 功能描述 | 安全注意事項 |
|------|----------|--------------|
| `/restart` | 重新啟動 OpenCode | 會保存當前會話 |
| `/shutdown` | 優雅關閉系統 | 等待所有操作完成 |
| `/upgrade` | 升級到最新版本 | 確保網路連接穩定 |
| `/reset` | 完全重置系統 | 會清除所有資料 |

#### ⚠️ **系統控制實戰**

```bash
# 重新啟動（保持會話）
/restart

# 優雅關閉
/shutdown

# 升級到最新版本
/upgrade
# 輸出: 正在檢查更新... 下載中... 安裝完成

# 完全重置（危險操作！）
/reset
# 確認: 這將清除所有配置和會話資料，確認嗎？ (y/N)
```

---

## 🎯 快捷鍵一覽

### ⌨️ **終端快捷鍵**

| 快捷鍵 | 功能 | 類型 |
|--------|------|------|
| `Ctrl+C` | 中斷當前操作 | 系統 |
| `Ctrl+D` | 退出程式 | 系統 |
| `Ctrl+L` | 清空螢幕 | 界面 |
| `Ctrl+X, H` | 顯示幫助 | 功能 |
| `Ctrl+X, Q` | 退出程式 | 功能 |
| `Ctrl+X, N` | 新建會話 | 功能 |
| `Ctrl+X, S` | 分享會話 | 功能 |
| `Ctrl+X, U` | 撤銷操作 | 功能 |
| `Ctrl+X, R` | 重做操作 | 功能 |

### 🎨 **輸入編輯快捷鍵**

| 快捷鍵 | 功能 | 說明 |
|--------|------|------|
| `Ctrl+A` | 移動到行首 | Emacs 風格 |
| `Ctrl+E` | 移動到行尾 | Emacs 風格 |
| `Ctrl+B` | 左移一個字符 | Backward |
| `Ctrl+F` | 右移一個字符 | Forward |
| `Alt+B` | 左移一個單詞 | Word backward |
| `Alt+F` | 右移一個單詞 | Word forward |
| `Ctrl+K` | 刪除到行尾 | Kill line |
| `Ctrl+U` | 刪除到行首 | Unix line erase |
| `Ctrl+W` | 刪除前一個單詞 | Word erase |

---

## 📊 常用組合和技巧

### 🎯 **高效工作流程**

#### **1. 快速開發流程**
```bash
# 1. 啟動並連接
opencode
/connect

# 2. 初始化專案
/init

# 3. 開發階段
> 請分析當前專案結構
> 建議改進架構
> 幫我實現新功能

# 4. 測試和優化
> 請撰寫測試用例
> 分析程式碼效能
```

#### **2. 學習和研究流程**
```bash
# 1. 切換到 Plan Mode
<Tab>

# 2. 研究階段
@general 請研究最新的前端框架趨勢

# 3. 實際實踐
<Tab>  # 切回 Build Mode
> 請根據研究結果創建一個範例專案
```

### 🎨 **進階提問技巧**

#### **📝 結構化提問**
```bash
# 使用項目符號組織複雜需求
> 請幫我創建一個完整的 React 應用，包含：
> • 使用者認證系統（登入/註冊）
> • 儀表板頁面
> • 資料管理功能
> • 響應式設計
> • TypeScript 支援
```

#### **🎯 指定輸出格式**
```bash
# 要求特定格式輸出
> 請用表格比較 Vue 3、React 18、Angular 17 的：
> • 學習曲線
> • 生態系統
> • 效能表現
> • 企業支援

# 要求程式碼區塊
> 請提供 TypeScript 介面定義範例
```

#### **🔍 提供充足上下文**
```bash
# 結合檔案引用和描述
> 請參考 @src/types/user.ts 中的型別定義，
> 並查看 @src/store/userSlice.ts 的狀態管理，
> 幫我在 @src/components/ 中創建一個完整的
> 使用者管理元件
```

---

## 🔧 故障排除命令

### ❌ **連接問題解決**

```bash
# 檢查網路連接
/health

# 重新連接提供商
/connect

# 刷新模型列表
/models --refresh

# 查看詳細錯誤日誌
/logs
```

### 🐛 **效能問題解決**

```bash
# 檢查系統資源
/doctor

# 切換到更快的模型
/model claude-3-haiku

# 清除歷史記錄
/clear

# 重啟系統
/restart
```

### 📁 **檔案權限問題**

```bash
# 檢查當前目錄
> 請顯示當前目錄的詳細資訊和權限

# 檢查特定檔案
> 請檢查 package.json 的檔案權限

# 嘗試修正權限
> 請修正當前目錄中所有檔案的權限為 644
```

---

## 🎉 總結與下步驟

### ✅ **你已經掌握了：**

- 🚀 **核心啟動命令** - opencode, run, help, version
- 🔑 **連接認證** - connect, auth, models, model
- 📁 **檔案操作** - @file, @dir/, read, list
- 🔄 **模式控制** - Tab, undo, redo, clear
- 📤 **分享協作** - share, unshare, export
- 🧠 **代理調用** - @agent, agent list
- ⚙️ **系統管理** - config, logs, restart, upgrade

### 🎯 **建議的練習方式：**

1. **日常使用** - 用 OpenCode 協助日常開發任務
2. **命令熟練** - 嘗試每個命令，熟悉其功能
3. **快捷鍵訓練** - 練習常用快捷鍵直到成為肌肉記憶
4. **場景應用** - 在不同場景下嘗試不同的命令組合

### 🚀 **準備好進階學習**

掌握了基本命令後，你已經準備好進入更高級的使用階段！

👉 **[繼續：使用指南 →](../usage/tui-interface.md)**

---

<div align="center">
  <p><strong>恭喜！你已經掌握 OpenCode 的核心命令，現在可以高效使用了！</strong></p>
  <p>💡 訣竅：熟能生巧，多練習不同的命令組合，發現更多可能性</p>
</div>