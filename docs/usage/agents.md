# 🤖 代理系統

> 深入了解 OpenCode 的智能代理系統，掌握 Build Agent、Plan Agent 和子代理的協作之道！

## 🧠 代理系統概覽

OpenCode 的代理系統是其最強大的特性之一。它不是單一的 AI，而是一個協作的智能體系統，每個代理都有特定的專長和工作方式。

### 🎯 **代理類型分類**

```
🏗️ 主代理系統
├── Build Agent    (建構代理) - 完整功能的主代理
└── Plan Agent     (規劃代理) - 安全分析專家

🧰 子代理系統  
├── General Agent  (通用代理) - 研究和分析專家
├── Explore Agent  (探索代理) - 快速搜索專家
├── Code Reviewer  (代碼審查) - 質量檢查專家
└── Custom Agents  (自定義代理) - 用戶定義的專家
```

## 🏗️ 主代理系統

### 🎯 **Build Agent - 建構代理**

#### **核心特徵**
- ✅ **完整功能** - 擁有所有工具權限
- ✅ **執行導向** - 專注於實際完成任務
- ✅ **檔案操作** - 可以讀取、寫入、修改檔案
- ✅ **系統命令** - 可以執行 bash 命令
- ✅ **網路存取** - 可以獲取外部資源

#### **最佳使用場景**
```bash
# 程式碼開發
> 請幫我實現一個完整的用戶認證系統

# 檔案操作
> 請創建 src/components/ 目錄並添加所有必要的元件

# 系統集成
> 請設定 Docker 配置並建置映像

# 自動化腳本
> 請創建一個自動部署腳本
```

#### **實際操作範例**
```
👤 你: 請幫我創建一個 Node.js 的 REST API

🤖 Build Agent: 我來幫你創建一個完整的 Node.js REST API

🔧 分析需求：Express 框架、CRUD 操作、錯誤處理、測試
📝 正在創建 package.json...
✅ 已創建 package.json
📝 正在創建 src/server.js...
✅ 已創建 src/server.js
📝 正在創建 src/routes/users.js...
✅ 已創建 src/routes/users.js
🔧 正在安裝依賴...
✅ 已安裝所有依賴
🧪 正在運行測試...
✅ 所有測試通過

API 已成功創建！可以運行 `npm start` 啟動服務器。
```

### 🎯 **Plan Agent - 規劃代理**

#### **核心特徵**
- ⚠️ **安全優先** - 檔案和命令操作需要詢問
- ✅ **分析專精** - 深度分析和理解能力
- ✅ **規劃導向** - 專注於設計和策略
- ✅ **風險評估** - 識別潛在問題和風險
- ✅ **替代方案** - 提供多種解決方案

#### **最佳使用場景**
```bash
# 架構設計
> 請設計一個微服務架構的電商系統

# 技術選型
> 請比較 React vs Vue vs Angular 的優劣

- 重構建議
> 請分析這個專案的架構並提供改進建議

# 安全評估
> 請評估當前系統的安全性問題
```

#### **實際操作範例**
```
👤 你: 請分析這個專案的架構並提供改進建議

🤖 Plan Agent: 我來分析這個專案的架構並提供改進建議

📊 架構分析：
- 當前架構：單體應用，Express + MongoDB
- 程式碼量：15K 行，3 個主要模組
- 問題識別：
  • 缺乏模組化設計
  • 沒有錯誤處理統一機制
  • 缺少測試覆蓋

🎯 改進建議：

1. **模組化重構**
   - 分離業務邏輯和資料存取
   - 引入依賴注入模式
   - 創建清晰的模組邊界

2. **錯誤處理統一**
   - 實現全域錯誤處理中間件
   - 標準化錯誤回應格式
   - 添加日誌記錄機制

3. **測試基礎設施**
   - 單元測試覆蓋率 80%
   - 集成測試自動化
   - CI/CD 管道建置

⚠️ 風險評估：
- 重構期間可能影響現有功能
- 需要團隊培訓適應新架構
- 建議分階段實施

要執行這個改進計劃嗎？(y/N)
```

## 🔄 模式切換策略

### 🎯 **何時使用 Build Mode**

#### **適合場景**
- ✅ 開發新功能
- ✅ 修復明確的 bug
- ✅ 重構已有程式碼
- ✅ 創建重複性內容
- ✅ 自動化工具腳本

#### **操作範例**
```bash
# 切換到 Build Mode（預設）
<Tab>

# 直接執行任務
> 請修復 src/auth.js 中的登入邏輯錯誤
> 請創建一個資料庫遷移腳本
> 請更新所有套件到最新版本
```

### 🎯 **何時使用 Plan Mode**

#### **適合場景**
- 🤔 架構設計和分析
- 🤔 技術選型和比較
- 🤔 重構策略規劃
- 🤔 風險評估和預測
- 🤔 最佳實踐研究

#### **操作範例**
```bash
# 切換到 Plan Mode
<Tab>

# 進行分析規劃
> 請分析這個 React 應用的性能瓶頸
> 請設計一個可擴展的微服務架構
> 請比較不同資料庫的適用性
```

### 🔄 **動態切換技巧**

#### **智能切換工作流**
```bash
# 1. 在 Plan Mode 分析
<Tab>  # 切換到 Plan Mode
> 請分析這個 API 的安全性問題

# 2. AI 提供詳細分析
🤖 Plan Agent: [詳細的問題分析和建議]

# 3. 切換到 Build Mode 執行
<Tab>  # 切換回 Build Mode  
> 好的，請按照分析的建議修復這些安全問題

# 4. AI 直接執行修復
🤖 Build Agent: [立即開始修復操作]
```

## 🧰 子代理系統

### 🎯 **General Agent - 通用代理**

#### **專業領域**
- 🔍 **深度研究** - 複雜概念和技術調研
- 📊 **資料分析** - 大量資訊的整理和總結
- 🌐 **跨領域知識** - 整合多個技術領域
- 🎓 **教學解釋** - 複雜概念的清晰說明

#### **調用方式**
```bash
# 方式一：明確調用
@general 請研究 WebAssembly 的最新發展趨勢

# 方式二：OpenCode 自動判斷
> 請深入分析區塊鏈技術的應用場景
# OpenCode 自動選擇 General Agent
```

#### **實際應用範例**
```
👤 你: @general 請研究 Edge Computing 的技術實現

🤖 General Agent: 我來為你深入研究 Edge Computing 的技術實現

📚 技術概覽：
- 定義：在資料來源附近處理資料的分散式計算模式
- 核心技術：容器化、微服務、5G、物聯網
- 主要廠商：AWS Greengrass, Azure IoT Edge, Google Cloud IoT

🏗️ 技術實現層次：

1. **設備層** (Device Layer)
   - 傳感器、執行器、閘道器
   - 輕量級作業系統 (FreeRTOS, Embedded Linux)
   - 實時處理能力

2. **邊緣節點層** (Edge Node Layer)  
   - 工業 PC、單板電腦、邊緣伺服器
   - 容器運行環境 (Docker, K3s)
   - 資料預處理和快取

3. **雲端協調層** (Cloud Orchestration Layer)
   - 集中管理和監控
   - 模型部署和更新
   - 資料同步和備份

🎯 實際應用場景：
- 工業物聯網預測性維護
- 自動駕駛即時決策
- 智慧城市交通優化
- 遠端醫療診斷輔助

📈 技術挑戰：
- 網路連接穩定性
- 資料安全和隱私
- 設備資源限制
- 運維管理複雜度

需要我深入探討某個特定方面嗎？
```

### 🔍 **Explore Agent - 探索代理**

#### **專業領域**
- ⚡ **快速搜索** - 檔案、內容、模式的快速定位
- 🗂️ **代碼導航** - 複雜代碼庫的高效導航
- 📋 **模式識別** - 代碼模式和設計模式的識別
- 🎯 **精準定位** - 快速找到特定功能的實現

#### **調用方式**
```bash
# 明確調用
@explore 找出專案中所有的 API 端點

# 自動調用（搜索類任務）
> 請找到所有處理用戶認證的檔案
# OpenCode 自動選擇 Explore Agent
```

#### **實際應用範例**
```
👤 你: @explore 請找出這個專案中所有與支付功能相關的程式碼

🤖 Explore Agent: 我來快速搜索專案中的支付相關程式碼

🔍 搜索結果：

**核心支付檔案 (5 個)**
1. `src/services/payment.js` - 主要支付邏輯
2. `src/api/routes/payment.js` - 支付 API 端點
3. `src/models/payment.js` - 支付資料模型
4. `src/middleware/payment.js` - 支付中介軟體
5. `src/utils/payment-validator.js` - 支付驗證工具

**相關配置檔案 (3 個)**
1. `config/payment-providers.json` - 支付服務商配置
2. `config/stripe.js` - Stripe 支付設定
3. `config/paypal.js` - PayPal 支付設定

**測試檔案 (4 個)**
1. `tests/unit/payment.test.js` - 單元測試
2. `tests/integration/payment-api.test.js` - API 集成測試
3. `tests/e2e/payment-flow.test.js` - 端到端測試
4. `fixtures/payment-data.js` - 測試資料

**關鍵功能分析：**
- 💳 支援 Stripe、PayPal、信用卡支付
- 🔒 實現 PCI DSS 安全標準
- 🔄 具備失敗重試機制
- 📊 詳細的支付記錄和報表

**潛在問題：**
- ⚠️ 測試覆蓋率僅 65%
- ⚠️ 缺少支付失敗回滾機制
- ⚠️ 配置檔案硬編碼敏感資訊

需要我詳細分析某個特定檔案或功能嗎？
```

## 🎨 自定義代理創建

### 🎯 **創建自定義代理**

#### **方法一：配置文件方式**
```json
{
  "$schema": "https://opencode.ai/config.json",
  "agent": {
    "security-expert": {
      "description": "資訊安全專家，專注於代碼安全審查和漏洞檢測",
      "mode": "subagent",
      "model": "anthropic/claude-sonnet-4-5",
      "temperature": 0.1,
      "tools": {
        "read": true,
        "write": false,
        "edit": false,
        "bash": false,
        "webfetch": true,
        "websearch": true
      }
    }
  }
}
```

#### **方法二：Markdown 文件方式**
創建 `.opencode/agent/security-expert.md`：

```markdown
---
name: security-expert
description: 資訊安全專家，專注於代碼安全審查和漏洞檢測
mode: subagent
model: anthropic/claude-sonnet-4-5
temperature: 0.1
tools:
  read: true
  write: false
  edit: false
  bash: false
---

# 資訊安全專家

## 核心職責
你是這個專案的資訊安全專家，專注於：

- **代碼安全審查** - 識別潛在的安全漏洞
- **漏洞檢測** - 使用業界最佳實踐檢查安全性
- **安全建議** - 提供具體的安全改進方案
- **合規檢查** - 確保符合安全標準和法規

## 安全檢查清單
- [ ] SQL 注入防護
- [ ] XSS 攻擊防護  
- [ ] CSRF 保護機制
- [ ] 身份認證和授權
- [ ] 資料加密和傳輸安全
- [ ] 日誌記錄和監控
- [ ] 第三方套件安全性

## 工作方式
你專注於分析和建議，不直接修改代碼。提供：
- 詳細的安全風險評估
- 具體的修復建議
- 優先級排序
- 預防措施建議
```

### 🎯 **使用自定義代理**

#### **調用方式**
```bash
# 調用自定義代理
@agent security-expert 請審查這個認證函數的安全性

# 簡化調用
@security-expert 請檢查整個專案的安全配置
```

#### **實際應用**
```
👤 你: @security-expert 請審查 @src/auth.js 的安全性

🤖 Security Expert: 我來詳細審查這個認證模組的安全性

🔍 安全審查結果：

**🚨 高風險問題 (3 個)**
1. **硬編碼密碼** - 第 15 行
   - 問題：密碼直接寫在程式碼中
   - 風險：極高，洩漏風險 100%
   - 建議：使用環境變數或金鑰管理服務

2. **不安全的密碼儲存** - 第 28 行
   - 問題：使用明文儲存密碼
   - 風險：極高，暴力破解風險高
   - 建議：使用 bcrypt 或 Argon2 雜湊

3. **缺乏 Rate Limiting** - 整體
   - 問題：沒有登入嘗試次數限制
   - 風險：高，易受暴力破解攻擊
   - 建議：實施登入頻率限制

**⚠️ 中風險問題 (2 個)**
1. **JWT 密鑰過弱** - 第 45 行
2. **缺乏輸入驗證** - 第 22 行

**✅ 安全最佳實踐 (2 個)**
1. 正確使用 HTTPS
2. 實施了基本的中介軟體

**🎯 優先修復建議：**
1. 立即：移除硬編碼密碼
2. 本週：實施密碼雜湊
3. 下週：加入 Rate Limiting

需要我提供詳細的修復代碼範例嗎？
```

## 🔄 代理協作模式

### 🎯 **串行協作**

```bash
# 1. Explore Agent 先搜索
@explore 找出所有處理使用者資料的檔案

# 2. General Agent 分析
@general 分析這些檔案的設計模式

# 3. Security Expert 審查
@security-expert 審查安全性問題

# 4. Build Agent 修復
<Tab>  # 切換到 Build Mode
> 請根據前面的分析和建議修復所有問題
```

### 🎯 **並行處理**

```bash
# 同時調用多個代理處理不同方面
@explore 分析前端的元件結構
@general 研究後端架構設計最佳實踐
@security-expert 檢查 API 安全性
```

### 🎯 **專家會議模式**

```bash
# 模擬多個專家討論同一問題
> 請組織一個技術討論：
> • Security Expert 提出安全要求
> • Performance Expert 提出性能指標  
> • UX Designer 提出用戶體驗需求
> • Architect 提供整合方案
```

## ⚡ 效率優化技巧

### 🎯 **選擇合適的代理**

#### **快速決策表**
| 任務類型 | 推薦代理 | 原因 |
|----------|----------|------|
| 檔案搜索 | Explore Agent | 快速定位和導航 |
| 深度研究 | General Agent | 跨領域知識整合 |
| 安全審查 | Security Expert | 專業安全知識 |
| 性能優化 | Performance Agent | 性能分析專精 |
| 代碼生成 | Build Agent | 完整執行能力 |

### 🎯 **代理組合策略**

#### **標準工作流程**
```bash
# 1. 快速探索問題
@explore 找出相關檔案和功能

# 2. 深度分析問題
@general 分析問題的根本原因

# 3. 專業建議
@specialist 提供專業解決方案

# 4. 實施解決方案
<Tab>  # Build Mode
> 請按照專家建議實施修復
```

#### **緊急修復流程**
```bash
# 1. 快速定位問題
@explore 找出錯誤的來源檔案

# 2. 直接修復
<Tab>  # Build Mode
> 請立即修復這個緊急問題
```

## 🔧 故障排除

### ❌ **代理選擇錯誤**

```bash
# 問題：用 Explore Agent 做深度研究
> @explore 請深入研究區塊鏈技術
# 解決：切換到 General Agent
> @general 請深入研究區塊鏈技術

# 問題：用 Build Agent 做架構設計
# 解決：切換到 Plan Mode
<Tab>  # 切換到 Plan Mode
```

### ❌ **代理響應不合預期**

```bash
# 明確指定代理的專業領域
@security-expert 請從資訊安全角度審查這個代碼

# 提供更多上下文和背景
@general 請分析這個前端專案的架構，
特別關注性能和可維護性
```

### 🎯 **最佳實踐建議**

1. **明確任務目標** - 清楚定義你希望代理做什麼
2. **提供充分上下文** - 給予代理足夠的背景資訊
3. **善用模式切換** - 根據任務性質選擇合適的模式
4. **組合使用代理** - 發揮不同代理的專業優勢
5. **迭代改進** - 根據結果調整策略和方法

---

## 🚀 下一步學習

現在 你已經完全掌握了 OpenCode 的代理系統！

👉 **[繼續：命令詳解 →](commands.md)**

---

<div align="center">
  <p><strong>恭喜！你已經成為 OpenCode 代理系統的專家！</strong></p>
  <p>💡 訣竅：選擇正確的代理能讓效率提升數倍</p>
</div>