# 🚀 OpenCode 完整使用指南

> **最全面的 OpenCode AI 編程助手中文使用指南**  
> 從入門到精通，讓 AI 成為你開發路上的最佳夥伴

[![GitHub stars](https://img.shields.io/github/stars/chilung-cgu/opencode-guide.svg?style=social&label=Star)](https://github.com/chilung-cgu/opencode-guide)
[![GitHub forks](https://img.shields.io/github/forks/chilung-cgu/opencode-guide.svg?style=social&label=Fork)](https://github.com/chilung-cgu/opencode-guide)
[![GitHub license](https://img.shields.io/github/license/chilung-cgu/opencode-guide.svg)](https://github.com/chilung-cgu/opencode-guide/blob/main/LICENSE)
[![Build Status](https://github.com/chilung-cgu/opencode-guide/workflows/Deploy%20MkDocs%20to%20GitHub%20Pages/badge.svg)](https://github.com/chilung-cgu/opencode-guide/actions)

## 📖 關於本指南

OpenCode 是一個開源的 AI 編程助手，支援 75+ 個 LLM 提供商，提供終端界面、桌面應用和 IDE 擴充功能。本指南旨在為中文用戶提供最完整、最實用的使用說明。

### 🎯 適合誰閱讀？

- **👶 完全新手** - 第一次接觸 AI 編程助手
- **💻 有經驗開發者** - 想要提升開發效率的程式設計師
- **🏢 企業用戶** - 需要團隊協作和企業級部署
- **📚 技術文檔撰寫者** - 需要了解 AI 輔助文檔創建
- **🔧 DevOps 工程師** - 需要整合到 CI/CD 流程

### ✨ 本指南特色

- **🔄 持續更新** - 緊跟 OpenCode 最新版本
- **💻 實戰導向** - 豐富的實際專案範例
- **🎨 視覺化教學** - 圖表、截圖、影片教學
- **🔧 深度解析** - 不只是表面操作，深入原理解說
- **🌐 社群驅動** - 歡迎貢獻和反饋

## 🚀 快速開始

### 安裝 OpenCode

```bash
# 自動安裝腳本（推薦）
curl -fsSL https://opencode.ai/install | bash

# 或使用 npm
npm install -g opencode-ai

# 或使用 Homebrew
brew install anomalyco/tap/opencode
```

### 第一次使用

```bash
# 1. 啟動 OpenCode
opencode

# 2. 連接 LLM 提供商
/connect

# 3. 初始化專案
cd /path/to/your/project
opencode
/init
```

## 📚 內容導航

### 🚀 快速開始
- [安裝配置](getting-started/installation.md) - 詳細的安裝和配置指南
- [第一次使用](getting-started/first-time.md) - 從零開始的入門教程
- [基本命令](getting-started/basic-commands.md) - 核心命令速查表

### 🔧 使用指南
- [TUI 界面](usage/tui-interface.md) - 終端用戶界面詳解
- [代理系統](usage/agents.md) - Build Agent vs Plan Agent
- [命令詳解](usage/commands.md) - 完整命令參考
- [最佳實踐](usage/best-practices.md) - 專業開發工作流程

### ⚙️ 配置詳解
- [主題設定](configuration/themes.md) - 個人化外觀配置
- [快捷鍵](configuration/keybinds.md) - 效率提升的按鍵配置
- [模型配置](configuration/models.md) - 75+ 提供商整合指南
- [自定義工具](configuration/custom-tools.md) - 擴展 OpenCode 功能

### 🚀 進階功能
- [技能系統](advanced/skills-system.md) - 創建可重用的行為模式
- [MCP 服務器](advanced/mcp-servers.md) - 整合外部服務
- [插件開發](advanced/plugins.md) - 自定義插件開發指南
- [企業部署](advanced/enterprise.md) - 企業級配置和管理

### 💡 實戰案例
- [Web 開發](examples/web-development.md) - 前端開發最佳實踐
- [API 開發](examples/api-development.md) - 後端開發完整流程
- [機器學習](examples/machine-learning.md) - AI 專案開發範例
- [團隊協作](examples/team-collaboration.md) - 多人開發工作流程

### 🔧 故障排除
- [常見問題](troubleshooting/common-issues.md) - 典型問題解決方案
- [調試技巧](troubleshooting/debugging.md) - 系統性問題診斷
- [效能優化](troubleshooting/performance.md) - 性能調優指南

## 🏗️ 專案架構

```
opencode-guide/
├── 📄 AGENTS.md              # AI 專家配置文件
├── ⚙️ opencode.json          # OpenCode 全域配置
├── 📖 README.md              # 專案說明（本檔案）
├── 📚 docs/                  # 文檔源碼
│   ├── getting-started/      # 快速開始
│   ├── usage/               # 使用指南
│   ├── configuration/       # 配置詳解
│   ├── advanced/           # 進階功能
│   ├── examples/           # 實戰案例
│   └── troubleshooting/    # 故障排除
├── .github/workflows/       # GitHub Actions 配置
└── mkdocs.yml              # MkDocs 配置文件
```

## 🤝 貢獻指南

我們歡迎所有形式的貢獻！

### 📝 如何貢獻

1. **Fork 本專案**
2. **創建功能分支** (`git checkout -b feature/amazing-feature`)
3. **提交變更** (`git commit -m 'Add some amazing feature'`)
4. **推送到分支** (`git push origin feature/amazing-feature`)
5. **開啟 Pull Request**

### 🎯 貢獻方向

- **📖 內容改進** - 錯誤修正、內容補充、範例優化
- **🌐 翻譯協助** - 英文內容翻譯、術語統一
- **🎨 視覺優化** - 圖表製作、截圖更新、美工設計
- **🔧 技術改進** - 文檔建置優化、部署流程改進
- **🐛 問題回報** - 發現問題、建議改進

### 📋 貢獻標準

- ✅ **技術準確** - 所有內容必須經過驗證
- ✅ **用戶友善** - 適合目標讀者的技術水平
- ✅ **格式一致** - 遵循既定的文檔風格
- ✅ **內容完整** - 提供完整的上下文和範例

## 📄 授權

本專案採用 [MIT 授權](LICENSE) - 歡迎自由使用和修改。

## 🔗 相關資源

### 官方資源
- [OpenCode 官網](https://opencode.ai)
- [GitHub 倉庫](https://github.com/anomalyco/opencode)
- [Discord 社群](https://opencode.ai/discord)
- [官方文檔](https://opencode.ai/docs)

### 社群資源
- [OpenCode Zen](https://opencode.ai/zen) - 經過驗證的模型推薦
- [YouTube 教學](https://youtube.com/playlist?list=...) - 影片教學資源
- [Reddit 社群](https://reddit.com/r/opencode) - 用戶討論

## 🙏 致謝

感謝以下貢獻者：

- [OpenCode 開發團隊](https://github.com/anomalyco/opencode) - 創造這個優秀的開源專案
- [所有貢獻者](https://github.com/chilung-cgu/opencode-guide/graphs/contributors) - 讓這份指南更加完整
- [社群成員](https://opencode.ai/discord) - 提供寶貴的反饋和建議

---

**🌟 如果這份指南對你有幫助，請給我們一個 Star！**

**💡 有問題或建議？歡迎 [開啟 Issue](https://github.com/chilung-cgu/opencode-guide/issues) 或加入討論！**

---

<div align="center">
  <p>使用 ❤️ 和 OpenCode 打造</p>
  <p>© 2025 OpenCode Guide 社群</p>
</div>