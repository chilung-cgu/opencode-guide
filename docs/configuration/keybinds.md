# ⌨️ 快捷鍵配置

> 掌握 OpenCode 的快捷鍵系統，讓你的開發效率倍增！

## 🎯 快捷鍵概覽

OpenCode 提供豐富的快捷鍵配置選項，讓你可以用鍵盤高效操控整個開發流程。無論是導航、編輯還是與 AI 互動，都可以透過快捷鍵快速完成。

### 🎹 **預設快捷鍵一覽**

#### **主要操作**
| 快捷鍵 | 功能 | 說明 |
|--------|------|------|
| `Tab` | 切換代理模式 | Build Mode ↔ Plan Mode |
| `Enter` | 送出訊息 | 將輸入的指令送出給 AI |
| `Ctrl+C` / `Cmd+C` | 取消操作 | 中斷當前執行的任務 |
| `Ctrl+L` / `Cmd+L` | 清除畫面 | 清除終端機畫面 |
| `Esc` | 取消輸入 | 清空當前輸入的內容 |

#### **導航快捷鍵**
| 快捷鍵 | 功能 | 說明 |
|--------|------|------|
| `↑` / `↓` | 歷史記錄 | 瀏覽之前輸入過的命令 |
| `Ctrl+Home` | 捲動到頂部 | 快速跳到對話最上方 |
| `Ctrl+End` | 捲動到底部 | 快速跳到對話最下方 |
| `Page Up` / `Page Down` | 翻頁 | 大範圍瀏覽對話內容 |

#### **編輯快捷鍵**
| 快捷鍵 | 功能 | 說明 |
|--------|------|------|
| `Ctrl+A` | 全選 | 選取輸入框中的所有內容 |
| `Ctrl+Backspace` | 刪除單字 | 刪除游標前的整個單字 |
| `Ctrl+W` | 刪除單字 | 同上（Unix 風格） |
| `Ctrl+U` | 刪除至行首 | 清除游標前的所有內容 |
| `Ctrl+K` | 刪除至行尾 | 清除游標後的所有內容 |

## ⚙️ 自定義快捷鍵

### 🎯 **配置文件設定**

在 `opencode.json` 中配置自定義快捷鍵：

```json
{
  "$schema": "https://opencode.ai/config.json",
  "keybinds": {
    "toggleMode": "Tab",
    "submit": "Enter",
    "cancel": "Ctrl+C",
    "clear": "Ctrl+L",
    "escape": "Escape",
    "historyUp": "ArrowUp",
    "historyDown": "ArrowDown",
    "scrollTop": "Ctrl+Home",
    "scrollBottom": "Ctrl+End",
    "selectAll": "Ctrl+A",
    "deleteWord": "Ctrl+Backspace",
    "deleteLine": "Ctrl+U"
  }
}
```

### 🎯 **進階配置範例**

#### **Vim 風格配置**
```json
{
  "keybinds": {
    "toggleMode": "Ctrl+Space",
    "historyUp": "Ctrl+K",
    "historyDown": "Ctrl+J",
    "scrollTop": "G",
    "scrollBottom": "Shift+G",
    "cancel": "Ctrl+C"
  }
}
```

#### **Emacs 風格配置**
```json
{
  "keybinds": {
    "deleteWord": "Alt+Backspace",
    "deleteLine": "Ctrl+U",
    "historyUp": "Ctrl+P",
    "historyDown": "Ctrl+N",
    "scrollTop": "Alt+<",
    "scrollBottom": "Alt+>"
  }
}
```

## 🎮 情境快捷鍵

### 🎯 **對話模式快捷鍵**

```
對話進行中：
  Tab        → 切換 Build/Plan 模式
  Enter      → 送出訊息
  ↑/↓        → 瀏覽歷史命令
  Ctrl+C     → 中斷當前任務
  Ctrl+L     → 清除畫面

輸入編輯：
  Ctrl+A     → 全選輸入內容
  Ctrl+U     → 清除輸入內容
  Ctrl+W     → 刪除前一個單字
  Home/End   → 跳到行首/行尾
```

### 🎯 **工具確認快捷鍵**

當 AI 請求執行工具時：

```
工具確認提示：
  Y/y/Enter  → 同意執行
  N/n        → 拒絕執行
  A/a        → 全部同意（本次會話）
  Ctrl+C     → 取消操作
```

### 🎯 **檔案操作快捷鍵**

當檢視或編輯檔案時：

```
檔案檢視：
  j/↓        → 向下捲動
  k/↑        → 向上捲動
  g          → 跳到頂部
  G          → 跳到底部
  q          → 退出檢視
```

## 🔧 快捷鍵衝突處理

### ❗ **常見衝突**

#### **終端機衝突**
```bash
# 問題：Ctrl+C 被終端機攔截
# 解決方案：使用 Ctrl+\ 作為替代

{
  "keybinds": {
    "cancel": "Ctrl+\\"
  }
}
```

#### **IDE 衝突**
```bash
# 問題：VS Code 快捷鍵衝突
# 解決方案：調整 OpenCode 的快捷鍵

{
  "keybinds": {
    "toggleMode": "Ctrl+Shift+Tab"
  }
}
```

### 🎯 **最佳實踐**

1. **避免與系統快捷鍵衝突** - 不要覆蓋 Ctrl+C、Ctrl+V 等常用系統快捷鍵
2. **保持一致性** - 如果習慣 Vim 或 Emacs，全部統一為同一風格
3. **記憶常用組合** - 先熟練使用 Tab、Enter、Ctrl+C 三個核心快捷鍵
4. **逐步自定義** - 先用預設配置，等熟悉後再根據需求調整

## 📋 快速參考卡

```
┌─────────────────────────────────────────────────────────┐
│                   OpenCode 快捷鍵卡                       │
├─────────────────────────────────────────────────────────┤
│  核心操作                                                 │
│    Tab         切換 Build/Plan 模式                       │
│    Enter       送出訊息                                   │
│    Ctrl+C      取消/中斷操作                               │
│    Ctrl+L      清除畫面                                   │
├─────────────────────────────────────────────────────────┤
│  歷史與導航                                               │
│    ↑/↓         瀏覽歷史命令                               │
│    Page Up/Dn  翻頁瀏覽                                   │
│    Ctrl+Home   跳到頂部                                   │
│    Ctrl+End    跳到底部                                   │
├─────────────────────────────────────────────────────────┤
│  編輯操作                                                 │
│    Ctrl+A      全選                                       │
│    Ctrl+U      清除行                                     │
│    Ctrl+W      刪除單字                                   │
│    Home/End    行首/行尾                                  │
└─────────────────────────────────────────────────────────┘
```

---

## 🚀 下一步學習

現在你已經掌握了 OpenCode 的快捷鍵配置！

👉 **[繼續：模型配置 →](models.md)**

---

<div align="center">
  <p><strong>🎹 鍵盤高手等級解鎖！</strong></p>
  <p>💡 訣竅：記住核心三鍵 Tab、Enter、Ctrl+C，效率立刻翻倍</p>
</div>
