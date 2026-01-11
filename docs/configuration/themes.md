# 🎨 主題設定

> 打造完全個人化的視覺體驗，從配色到字體，讓 OpenCode 成為你獨一無二的開發環境！

## 🎨 主題系統概覽

OpenCode 提供了豐富的主題系統，讓你打造最適合個人喜好和工作習慣的視覺環境。

### 📋 **主題類型**

```
🌙 深色主題      - 護眼，適合長時間工作
☀️ 淺色主題      - 清爽，適合日間工作
🎭 特殊主題      - 獨特風格，展現個性
🛠️ 自定義主題    - 完全個人化設計
```

---

## 🌙 內建深色主題

### 🎯 **TokyoNight** - 推薦深色主題

#### **特色**
- 基於流行的 Tokyo Night VSCode 主題
- 專業的配色方案，適合長時間編程
- 優秀的語法高亮對比度
- 舒適的暗色背景，減少眼部疲勞

#### **配色方案**
```json
{
  "colors": {
    "background": "#1a1b26",
    "foreground": "#c0caf5",
    "primary": "#7aa2f7",
    "secondary": "#9ece6a",
    "accent": "#e0af68",
    "warning": "#f7768e",
    "error": "#db4b4b",
    "success": "#9ece6a",
    
    // 語法高亮
    "syntaxKeyword": "#bb9af7",
    "syntaxString": "#9ece6a",
    "syntaxComment": "#565f89",
    "syntaxFunction": "#7aa2f7",
    "syntaxVariable": "#c0caf5",
    "syntaxType": "#7dcfff"
  }
}
```

#### **適用場景**
- 長時間的開發工作
- 深夜或光線較暗的環境
- 需要高度專注的編程任務
- 前端開發和 UI 設計

#### **使用方式**
```bash
# 切換到 TokyoNight 主題
/config set theme tokyonight

# 或在啟動時指定
opencode --theme tokyonight
```

### 🌌 **GruvBox** - 復古深色主題

#### **特色**
- 溫暖的復古配色方案
- 高對比度，便於程式碼閱讀
- 獨特的黃綠色調
- 適合各種程式語言

#### **使用方式**
```bash
/config set theme gruvbox
```

### 🔵 **One Dark** - 經典深色主題

#### **特色**
- 來自 Atom 的經典主題
- 專業的藍灰色調
- 清晰的層次結構
- 廣受開發者喜愛

#### **使用方式**
```bash
/config set theme one-dark
```

---

## ☀️ 內建淺色主題

### 🌟 **Default** - 標準淺色主題

#### **特色**
- 清爽簡潔的設計
- 高可讀性的淺色背景
- 適合日間工作
- 標準化的配色方案

#### **使用方式**
```bash
/config set theme default
```

### 🌼 **Catppuccin Latte** - 溫柔淺色主題

#### **特色**
- 溫和的粉彩色調
- 舒適的視覺體驗
- 現代化的設計風格
- 深受年輕開發者喜愛

#### **使用方式**
```bash
/config set theme catppuccin-latte
```

---

## 🎭 特殊主題

### 💻 **Matrix** - 黑客風格

#### **特色**
- 經典的黑客帝國風格
- 綠色文字配黑色背景
- 獨特的視覺效果
- 充滿科技感

#### **使用方式**
```bash
/config set theme matrix
```

### 🌈 **Ayu** - 現代簡約

#### **特色**
- 現代簡約的設計理念
- 精心調配的色彩搭配
- 優秀的視覺層次
- 適合多種工作場景

#### **使用方式**
```bash
/config set theme ayu
```

---

## 🛠️ 自定義主題

### 🎨 **創建自定義主題**

#### **方法一：配置檔案方式**

```json
// ~/.config/opencode/themes/my-theme.json
{
  "$schema": "https://opencode.ai/theme.json",
  "name": "my-custom-theme",
  "description": "我的個人化主題",
  "author": "Your Name",
  "version": "1.0.0",
  
  "colors": {
    "background": {
      "dark": "#1e1e1e",
      "light": "#ffffff"
    },
    "foreground": {
      "dark": "#d4d4d4",
      "light": "#333333"
    },
    "primary": {
      "dark": "#007acc",
      "light": "#0066cc"
    },
    "secondary": {
      "dark": "#6c757d",
      "light": "#6c757d"
    },
    "success": {
      "dark": "#28a745",
      "light": "#28a745"
    },
    "warning": {
      "dark": "#ffc107",
      "light": "#ffc107"
    },
    "error": {
      "dark": "#dc3545",
      "light": "#dc3545"
    },
    "info": {
      "dark": "#17a2b8",
      "light": "#17a2b8"
    },
    
    // 語法高亮顏色
    "syntaxKeyword": {
      "dark": "#569cd6",
      "light": "#0000ff"
    },
    "syntaxString": {
      "dark": "#ce9178",
      "light": "#a31515"
    },
    "syntaxComment": {
      "dark": "#6a9955",
      "light": "#008000"
    },
    "syntaxFunction": {
      "dark": "#dcdcaa",
      "light": "#795e26"
    },
    "syntaxVariable": {
      "dark": "#9cdcfe",
      "light": "#001080"
    },
    "syntaxType": {
      "dark": "#4ec9b0",
      "light": "#267f99"
    },
    "syntaxNumber": {
      "dark": "#b5cea8",
      "light": "#098658"
    },
    "syntaxOperator": {
      "dark": "#d4d4d4",
      "light": "#000000"
    }
  },
  
  "ui": {
    "border": {
      "dark": "#3c3c3c",
      "light": "#e0e0e0"
    },
    "selection": {
      "dark": "#264f78",
      "light": "#add8e6"
    },
    "cursor": {
      "dark": "#a6a6a6",
      "light": "#000000"
    },
    "highlight": {
      "dark": "#2d2d30",
      "light": "#f0f0f0"
    }
  },
  
  "fonts": {
    "family": "JetBrains Mono",
    "size": 14,
    "weight": "normal",
    "lineHeight": 1.4
  },
  
  "spacing": {
    "margin": 4,
    "padding": 8,
    "gap": 2
  }
}
```

#### **方法二：快速自定義**

```bash
# 基於現有主題快速調整
/config set theme base tokyonight
/config set theme.colors.primary "#ff6b6b"
/config set theme.colors.secondary "#4ecdc4"
/config set theme.font.size 16
```

### 🎯 **主題命名規範**

#### **推薦命名方式**
```bash
# 個人主題
my-dark-theme
my-light-theme
developer-theme

# 團隊主題
company-dev-theme
team-frontend-theme
organization-standard

# 功能主題
low-light-theme          # 低光線環境
high-contrast-theme      # 高對比度
accessibility-theme      # 無障礙友好
```

---

## 🔧 高級主題配置

### 🎨 **動態主題切換**

#### **時間自動切換**
```bash
# 設定自動切換
/config set theme.auto_switch true
/config set theme.day_theme "default"
/config set theme.night_theme "tokyonight"
/config set theme.switch_time "18:00"  # 晚上 6 點切換
```

#### **環境光感應切換**
```bash
# 基於環境光線自動切換（需要硬體支援）
/config set theme.ambient_light_sensor true
/config set theme.brightness_threshold 0.5
```

### 🌈 **主題動畫效果**

#### **漸變過渡效果**
```bash
# 啟用主題切換動畫
/config set theme.transition_duration 300
/config set theme.transition_type "fade"  # fade, slide, none
```

#### **顏色動畫**
```bash
# 啟用彩色動畫效果
/config set theme.color_animations true
/config set theme.animation_speed "normal"  # slow, normal, fast
```

---

## 🎯 主題最佳實踐

### 👀 **視覺舒適性**

#### **護眼配置**
```bash
# 藍光過濾
/config set theme.blue_light_filter true
/config set theme.filter_strength 0.3

# 畫面亮度調整
/config set theme.brightness 0.9
/config set theme.contrast 1.1
```

#### **字體優化**
```bash
# 減少眼睛疲勞的字體設定
/config set font.family "IBM Plex Mono"
/config set font.size 14
/config set font.line_height 1.6
/config set font.letter_spacing 0.1
```

### 🎨 **工作環境優化**

#### **根據工作類型選擇主題**
```bash
# 前端開發 - 高色彩還原
/config set theme "catppuccin"

# 後端開發 - 專業穩重
/config set theme "tokyonight"

# 數據分析 - 高對比度
/config set theme "gruvbox"

# 創意工作 - 溫和色調
/config set theme "ayu"
```

#### **時間段主題配置**
```bash
# 早上 (6:00-12:00) - 淺色主題
# 下午 (12:00-18:00) - 標準主題  
# 晚上 (18:00-6:00) - 深色主題

/config set theme.schedule.morning "default"
/config set theme.schedule.afternoon "one-dark"
/config set theme.schedule.evening "tokyonight"
```

---

## 🔍 主題故障排除

### ❌ **常見問題**

#### **主題載入失敗**
```bash
# 檢查主題檔案
/config validate theme my-theme

# 重新載入主題
/config reload theme

# 恢復預設主題
/config reset theme
```

#### **顏色顯示異常**
```bash
# 檢查終端色彩支援
/doctor terminal-colors

# 設定色彩模式
/config set terminal.color_mode truecolor  # 256, truecolor

# 重置色彩配置
/config reset colors
```

#### **字體顯示問題**
```bash
# 檢查字體可用性
/doctor fonts

# 設定備用字體
/config set font.fallback "monospace"

# 重置字體配置
/config reset font
```

### 🛠️ **調試技巧**

#### **主題預覽**
```bash
# 預覽主題效果
/config theme preview my-theme

# 對比主題差異
/config theme compare tokyonight one-dark

# 導出主題配置
/config theme export my-theme.json
```

---

## 🌐 社群主題

### 🎨 **熱門社群主題**

#### **Dracula** - 經典深色主題
```bash
# 安裝 Dracula 主題
/config theme install dracula

# 使用主題
/config set theme dracula
```

#### **Nord** - 北歐風格主題
```bash
# 安裝 Nord 主題
/config theme install nord

# 使用主題
/config set theme nord
```

#### **Monokai** - 經典程式設計主題
```bash
# 安裝 Monokai 主題
/config theme install monokai

# 使用主題
/config set theme monokai
```

### 🔄 **主題分享和下載**

#### **分享個人主題**
```bash
# 打包主題
/config theme package my-theme

# 分享到社群
/config theme share my-theme --platform github
```

#### **下載社群主題**
```bash
# 搜索主題
/config theme search "high contrast"

# 下載主題
/config theme download high-contrast-theme

# 安裝主題
/config theme install high-contrast-theme
```

---

## 🎉 主題配置總結

### ✅ **配置建議**

1. **個人化優先** - 選擇最適合個人喜好和習慣的主題
2. **舒適性考慮** - 優先考慮長時間使用的舒適性
3. **環境適應** - 根據工作環境調整主題設定
4. **定期更新** - 關注新的主題和配色方案

### 🎯 **進階技巧**

1. **主題組合** - 為不同工作場景創建主題組合
2. **動態調整** - 根據時間和環境自動調整主題
3. **社群參與** - 分享個人主題，參與社群討論
4. **持續優化** - 根據使用體驗持續優化主題配置

---

## 🚀 下一步學習

現在 你已經完全掌握了 OpenCode 的主題系統！

👉 **[繼續：快捷鍵設定 →](keybinds.md)**

---

<div align="center">
  <p><strong>恭喜！你已經成為 OpenCode 主題設計的專家！</strong></p>
  <p>💡 訣竅：找到最適合自己的主題，讓編程成為一種享受</p>
</div>