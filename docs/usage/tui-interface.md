# 🎮 TUI 界面詳解

> 掌握 OpenCode 的終端用戶界面，從基礎操作到進階技巧，讓你的工作效率飆升！

## 🎯 TUI 界面概覽

OpenCode 的 TUI（Terminal User Interface）設計精良，既簡潔又功能強大。讓我們全面了解每個組件和功能。

### 📱 **界面結構解析**

```
┌─────────────────────────────────────────────────────────────────────┐
│ OpenCode - The open source AI coding agent              [Help: Ctrl+X,H] │
│                                                                     │
│ ┌─────────────────────────────────────────────────────────────────┐ │
│ │ > 在這裡輸入你的問題或命令...                                   │ │
│ └─────────────────────────────────────────────────────────────────┘ │
│                                                                     │
│ 🎯 你: 請幫我創建一個 REST API                                     │
│ 🤖 AI: 我來幫你創建一個完整的 REST API...                          │
│                                                                     │
│    ✅ 已創建 api/index.js                                          │
│    ✅ 已創建 package.json 的依賴更新                               │
│    🔧 正在配置 Express 伺服器...                                   │
│                                                                     │
│ [Build Mode] │ [Connected: opencode] │ [Model: claude-3-haiku]      │
│ [Session: default] │ [Tokens: 1.2K/200K] │ [Time: 00:05:23]          │
└─────────────────────────────────────────────────────────────────────┘
```

#### 📍 **主要區域說明**

| 區域 | 功能 | 交互方式 |
|------|------|----------|
| **標題列** | 顯示應用程式名稱和快速幫助 | 靜態資訊顯示 |
| **輸入區** | 用戶輸入問題和命令的文字區 | 鍵盤輸入、編輯 |
| **對話區** | 顯示 AI 對話和操作歷史 | 滾動查看、複製 |
| **狀態列** | 顯示當前模式和系統狀態 | 即時更新、點擊交互 |

## ⌨️ 輸入區域操作

### 🎯 **基本輸入技巧**

#### **文字編輯**
```bash
# 移動光標
Ctrl+A    # 移動到行首
Ctrl+E    # 移動到行尾
Ctrl+B    # 向左移動一個字符
Ctrl+F    # 向右移動一個字符
Alt+B     # 向左移動一個單詞
Alt+F     # 向右移動一個單詞

# 刪除操作
Ctrl+K    # 刪除到行尾
Ctrl+U    # 刪除到行首
Ctrl+W    # 刪除前一個單詞
Ctrl+D    # 刪除光標處字符

# 歷史記錄
Ctrl+P    # 上一個命令（Up）
Ctrl+N    # 下一個命令（Down）
```

#### **快速補全和建議**
```bash
# 檔案路徑補全
@src/comp<Tab>  # 補全為 @src/components/
@package.json    # 直接補全檔案名

# 命令補全
/conn<Tab>      # 補全為 /connect
/mod<Tab>       # 補全為 /models

# 檔案內容預覽
@README.md<Tab> # 顯示檔案預覽
```

### 🎨 **進階輸入功能**

#### **多行輸入**
```bash
# Shift+Enter 開始多行輸入
> 請創建一個 Python 函數，包含以下功能：Shift+Enter
> - 計算數字列表的平均值Shift+Enter
> - 處理空列表的例外情況Shift+Enter
> - 返回浮點數結果Enter

# 自動識別多行輸入（無需 Shift+Enter）
> 請幫我創建一個 JavaScript 類別：
class User {
  constructor(name, email) {
    this.name = name;
    this.email = email;
  }
}
```

#### **快速命令插入**
```bash
# Ctrl+X, C 快速插入命令
Ctrl+X, C  # 顯示命令選單
# 使用方向鍵選擇，Enter 確認

# 常用快速插入
Ctrl+X, S  # 快速插入 /share
Ctrl+X, H  # 快速插入 /help
Ctrl+X, M  # 快速插入 /models
```

## 💬 對話區域功能

### 📊 **訊息類型識別**

OpenCode 的對話區顯示多種類型的訊息：

#### **👤 用戶訊息**
```
👤 你: 請幫我分析這段程式碼的效能問題
```

#### **🤖 AI 回應**
```
🤖 AI: 我來幫你分析這段程式碼的效能問題...
```

#### **🔧 系統操作**
```
🔧 正在讀取檔案: src/main.js
🔧 已分析完成，發現 3 個潛在問題
```

#### **✅ 成功操作**
```
✅ 已創建檔案: src/utils/performance.js
✅ 已更新依賴: package.json
```

#### **❌ 錯誤訊息**
```
❌ 無法讀取檔案: nonexistent.js
❌ 權限不足，無法修改 /etc/hosts
```

#### **💡 資訊提示**
```
💡 建議：使用 async/await 替代回調函數
💡 提示：該檔案已在其他編輯器中開啟
```

### 🎯 **互動式操作**

#### **程式碼區塊操作**
```
🤖 AI: 這是一個優化的範例：

```python
def calculate_average(numbers):
    # [Copy] [Run] [Edit] [Explain]
    if not numbers:
        return 0.0
    return sum(numbers) / len(numbers)
```
```

**可執行操作：**
- `Click [Copy]` - 複製程式碼到剪貼簿
- `Click [Run]` - 直接執行程式碼
- `Click [Edit]` - 編輯程式碼
- `Click [Explain]` - 請 AI 解釋程式碼

#### **檔案操作確認**
```
🤖 AI: 我即將執行以下操作：

📁 創建檔案: src/api/routes.js
📝 寫入內容: Express 路由定義（128 行）
🔧 更新依賴: package.json

[執行] [修改] [取消] [詳細]
```

**選項說明：**
- `[執行]` - 按原計劃執行
- `[修改]` - 修改操作內容
- `[取消]` - 取消當前操作
- `[詳細]` - 查看詳細操作資訊

## 📊 狀態列詳解

### 🎯 **模式指示器**

```
[Build Mode]     # 可修改檔案、執行命令
[Plan Mode]      # 僅規劃，需要確認
[Research Mode]  # 深度研究模式
[Debug Mode]     # 調試模式
```

#### **模式切換顯示**
```
Plan Mode → Build Mode  (切換成功)
Build Mode → Plan Mode  (切換成功)
```

### 🔗 **連接狀態**

```
[Connected: opencode]     # 已連接 OpenCode Zen
[Connected: openai]       # 已連接 OpenAI
[Connected: none]         # 未連接任何提供商
[Reconnecting...]         # 重新連接中
```

### 🤖 **模型資訊**

```
[Model: claude-3-haiku]          # 當前使用的模型
[Model: gpt-4o]                   # 當前使用的模型
[Switching: gpt-4o-mini...]      # 正在切換模型
```

### 📈 **使用統計**

```
[Tokens: 1.2K/200K]      # 已使用/總限制
[Cost: $0.018]            # 本次會話成本
[Time: 00:05:23]          # 會話持續時間
[Messages: 12]             # 訊息數量
```

## 🎨 界面自定義

### 🎯 **主題配置**

#### **內建主題**
```bash
# 切換主題
/config set theme tokyonight    # 深色主題
/config set theme default       # 淺色主題
/config set theme matrix         # 黑客風格
/config set theme catppuccin     # Catppuccin 主題
```

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
      "error": "#dc3545"
    }
  }
}
```

### 🔧 **界面佈局調整**

#### **字體和尺寸**
```bash
# 調整字體大小
/config set font_size 14

# 調整行間距
/config set line_height 1.2

# 調整邊距
/config set margin 4
```

#### **顯示選項**
```bash
# 顯示/隱藏行號
/config set show_line_numbers true

# 顯示/隱藏狀態列
/config set show_status_bar true

# 顯示/隱藏標題列
/config set show_title_bar true
```

## ⚡ 高效操作技巧

### 🎯 **快速導航**

#### **頁面導航**
```bash
# 滾動操作
PageUp     # 向上滾動一頁
PageDown   # 向下滾動一頁
Home       # 滾動到對話開始
End        # 滾動到對話結尾

# 跳轉到特定訊息
Ctrl+G     # 輸入行號跳轉
Ctrl+L     # 清空對話顯示區
```

#### **搜尋功能**
```bash
# 搜尋對話內容
Ctrl+F     # 開始搜尋
Ctrl+R     # 反向搜尋
F3         # 下一個匹配項
Shift+F3   # 上一個匹配項

# 搜尋檔案內容
Ctrl+X, F  # 搜尋檔案名稱
Ctrl+X, C  # 搜尋檔案內容
```

### 🎨 **複製和編輯**

#### **內容複製**
```bash
# 複製當前輸入
Ctrl+C     # 複製輸入區內容
Ctrl+X, C  # 複製程式碼區塊

# 複製對話內容
Ctrl+X, Y  # 複製 AI 回應
Ctrl+X, U  # 複製用戶輸入
```

#### **快速編輯**
```bash
# 編輯上一個輸入
Ctrl+X, E  # 編輯上一個命令
Ctrl+P     # 載入上一個命令到輸入區

# 快速插入常用內容
Ctrl+X, 1  # 插入常用模板 1
Ctrl+X, 2  # 插入常用模板 2
```

### 🚀 **批次操作**

#### **多命令執行**
```bash
# 使用分號分隔多個命令
> /model claude-3-haiku; 請分析這個檔案; @package.json

# 使用管道連接命令
> 請分析 @src/index.js | 請總結發現的問題
```

#### **腳本化操作**
```bash
# 執行預設腳本
> /run-script setup-project

# 執行自定義腳本
> /run-script ./scripts/analyze-project.sh
```

## 🔧 進階功能

### 🤖 **智能預測**

#### **輸入預測**
```
> 請幫我創建一個 React
└─ 🧠 預測: 元件、應用程式、鉤子、類別...
```

#### **命令建議**
```
> /con
└─ 💡 建議: /connect, /config, /clear
```

#### **檔案建議**
```
> @src/util
└─ 📁 建議: @src/utils/, @src/utilities/, @src/util.js
```

### 📊 **即時統計**

#### **性能監控**
```
🚀 當前響應時間: 1.2s
💾 記憶體使用: 45MB
🌐 網路延遲: 120ms
```

#### **成本追蹤**
```
💰 本次對話成本: $0.025
💰 今日總成本: $1.23
💰 本月預算: $10.00 (剩餘 $8.77)
```

### 🎯 **上下文管理**

#### **對話歷史**
```bash
# 查看對話歷史
/history

# 清空歷史
/clear-history

# 導出歷史
/export-history markdown > conversation.md
```

#### **上下文優化**
```bash
# 壓縮上下文
/compress-context

# 重置上下文
/reset-context

# 保存當前上下文
/save-context my-session
```

## 🔍 故障排除

### ❌ **界面問題**

#### **顯示異常**
```bash
# 檢查終端相容性
/doctor terminal

# 重置界面
/reset-interface

# 切換到簡化模式
/config set simple_mode true
```

#### **輸入問題**
```bash
# 檢查輸入法
/config show input_method

# 重置輸入緩衝
/reset-input

# 檢查鍵盤映射
/config show keybindings
```

### 🐛 **性能問題**

#### **響應緩慢**
```bash
# 檢查系統資源
/system-status

# 切換到更快的模型
/model claude-3-haiku

# 啟用緩存模式
/config set cache_enabled true
```

#### **記憶體不足**
```bash
# 檢查記憶體使用
/memory-status

# 清理快取
/clear-cache

# 降低歷史記錄限制
/config set history_limit 100
```

## 🎉 最佳實踐總結

### ✅ **高效工作流程**

1. **快速啟動** - 使用快捷鍵快速導航
2. **智能輸入** - 善用自動補全和預測
3. **多任務處理** - 靈活運用模式切換
4. **批量操作** - 使用命令組合提高效率

### 🎯 **個人化配置**

1. **主題選擇** - 選擇舒適的視覺主題
2. **快捷鍵設定** - 配置個人常用的快捷鍵
3. **界面佈局** - 調整合適的字體和間距
4. **功能開關** - 根據需求開啟/關閉特定功能

### 🚀 **進階技巧**

1. **腳本化** - 創建重複性操作的腳本
2. **自動化** - 設定觸發條件和自動響應
3. **整合工具** - 與其他開發工具無縫整合
4. **性能優化** - 持續監控和優化使用效率

---

## 🚀 下一步學習

現在 你已經完全掌握了 TUI 界面的所有功能！

👉 **[繼續：代理系統深入理解 →](agents.md)**

---

<div align="center">
  <p><strong>恭喜！你已經成為 OpenCode TUI 的專家級用戶！</strong></p>
  <p>💡 訣竅：持續練習和個人化配置，讓界面真正為你服務</p>
</div>