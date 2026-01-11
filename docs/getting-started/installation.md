# 🔧 安裝配置

> 在你的系統上安裝 OpenCode 並完成初始配置，準備開始你的 AI 輔助開發之旅！

## 🚀 快速安裝

### 🎯 推薦方式：自動安裝腳本

```bash
curl -fsSL https://opencode.ai/install | bash
```

這個腳本會自動：
- 🖥️ 檢測你的作業系統和架構
- 📦 下載最新版本的 OpenCode
- 🔧 設置系統路徑和環境變數
- ✅ 驗證安裝是否成功

### 📦 套件管理器安裝

#### Node.js 生態系
```bash
# npm
npm install -g opencode-ai

# Yarn  
yarn global add opencode-ai

# pnpm
pnpm add -g opencode-ai

# Bun
bun install -g opencode-ai
```

#### 系統套件管理器
```bash
# macOS (Homebrew)
brew install anomalyco/tap/opencode

# Linux (Paru, Arch Linux)
paru -S opencode-bin

# Windows (Chocolatey)
choco install opencode

# Windows (Scoop)
scoop bucket add extras
scoop install extras/opencode
```

## 📋 詳細安裝指南

### 🍎 macOS 安裝

#### 方法一：Homebrew（推薦）
```bash
# 安裝 Homebrew（如果還沒有）
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# 安裝 OpenCode
brew install anomalyco/tap/opencode

# 驗證安裝
opencode --version
```

#### 方法二：npm
```bash
# 安裝 Node.js（如果還沒有）
brew install node

# 安裝 OpenCode
npm install -g opencode-ai

# 驗證安裝
opencode --version
```

### 🪟 Windows 安裝

#### 方法一：Chocolatey（推薦）
```powershell
# 安裝 Chocolatey（如果還沒有）
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))

# 安裝 OpenCode
choco install opencode

# 驗證安裝
opencode --version
```

#### 方法二：npm
```powershell
# 安裝 Node.js（如果還沒有）
# 前往 https://nodejs.org 下載並安裝 LTS 版本

# 安裝 OpenCode
npm install -g opencode-ai

# 驗證安裝
opencode --version
```

### 🐧 Linux 安裝

#### Ubuntu/Debian
```bash
# 更新套件列表
sudo apt update

# 安裝必要的依賴
sudo apt install -y curl gnupg2

# 方法一：自動安裝腳本
curl -fsSL https://opencode.ai/install | bash

# 方法二：npm（需要先安裝 Node.js）
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
sudo apt-get install -y nodejs
npm install -g opencode-ai

# 驗證安裝
opencode --version
```

#### Arch Linux
```bash
# 安裝 Paru（AUR helper）
sudo pacman -S --needed git base-devel
git clone https://aur.archlinux.org/paru.git
cd paru
makepkg -si

# 安裝 OpenCode
paru -S opencode-bin

# 驗證安裝
opencode --version
```

## 🐳 Docker 安裝

### 基本使用
```bash
# 直接運行
docker run -it --rm ghcr.io/anomalyco/opencode

# 掛載當前目錄
docker run -it --rm -v $(pwd):/workspace ghcr.io/anomalyco/opencode

# 持續運行並保持狀態
docker run -d --name opencode -v opencode-data:/root/.local/share/opencode -v $(pwd):/workspace ghcr.io/anomalyco/opencode
```

### Docker Compose
```yaml
# docker-compose.yml
version: '3.8'
services:
  opencode:
    image: ghcr.io/anomalyco/opencode
    stdin_open: true
    tty: true
    volumes:
      - .:/workspace
      - opencode-data:/root/.local/share/opencode
    working_dir: /workspace
```

```bash
# 啟動服務
docker-compose up opencode

# 停止服務
docker-compose down
```

## ✅ 安裝驗證

### 基本驗證
```bash
# 檢查版本
opencode --version

# 檢查幫助資訊
opencode --help

# 檢查可用模型（需要先配置）
opencode models
```

### 功能測試
```bash
# 測試基本功能（需要先配置提供商）
opencode run "你好，請用繁體中文回應，並介紹你自己"
```

### 終端相容性測試
```bash
# 測試終端支援
echo -e "\033[31m紅色文字\033[0m \033[32m綠色文字\033[0m"

# 如果正常顯示顏色，你的終端完全相容
```

## ⚙️ 初始配置

### 🔑 選擇 LLM 提供商

#### 🌟 推薦新手：OpenCode Zen

1. **訪問 [opencode.ai/auth](https://opencode.ai/auth)**
2. **創建帳戶**或**使用現有帳戶登入**
3. **添加付款方式**（支援信用卡、PayPal）
4. **生成 API 金鑰**

**優點：**
- ✅ 團隊測試的高品質模型
- ✅ 統一的 API 和計費
- ✅ 簡單易懂的定價
- ✅ 與 OpenCode 深度整合

#### 🔧 其他熱門選擇

##### OpenAI
```bash
# 在 OpenCode TUI 中
/connect
# 選擇 OpenAI
# 輸入 API 金鑰（sk-...）
```

##### Anthropic Claude
```bash
/connect
# 選擇 Claude
# 輸入 API 金鑰（sk-ant-...）
```

##### Google Vertex AI
```bash
/connect
# 選擇 Google Vertex AI
# 按照指示完成 OAuth 認證
```

### 🎯 首次配置流程

```bash
# 1. 啟動 OpenCode TUI
opencode

# 2. 在 TUI 中連接提供商
/connect

# 3. 選擇你的提供商
# （使用方向鍵選擇，Enter 確認）

# 4. 輸入 API 金鑰
# （貼上你的 API 金鑰，Enter 確認）

# 5. 測試連接
opencode run "你好，請介紹你自己"
```

### 🔧 環境變數配置

#### 可選：設定預設模型
```bash
# 添加到 ~/.bashrc, ~/.zshrc, 或 ~/.profile
export OPENCODE_MODEL="anthropic/claude-sonnet-4-5"
export OPENCODE_SMALL_MODEL="anthropic/claude-haiku-4-5"
```

#### 可選：設定配置檔案位置
```bash
export OPENCODE_CONFIG_DIR="$HOME/.config/opencode"
export OPENCODE_CONFIG="$HOME/.config/opencode/opencode.json"
```

## 🏗️ 系統整合

### 🐚 Shell 整合

#### Bash/Zsh 整合
```bash
# 添加到 ~/.bashrc 或 ~/.zshrc
# OpenCode 別名
alias oc='opencode'
alias occ='opencode run --continue'
alias ocm='opencode models'

# OpenCode 在專案目錄中快速啟動
alias ocp='opencode --session $(basename $(pwd))'

# 快速功能別名
alias ocreview='opencode run "請審查這個檔案的品質："'
alias ocdoc='opencode run "請為這段程式碼撰寫文檔："'
```

#### PowerShell 整合
```powershell
# 添加到 PowerShell Profile ($PROFILE)
Set-Alias -Name oc -Value opencode
Set-Alias -Name occ -Value "opencode run --continue"
Set-Alias -Name ocm -Value "opencode models"

# 函數：在專案目錄快速啟動
function ocproj {
    opencode --session (Split-Path -Leaf $PWD)
}
```

### 🎨 終端主題優化

#### 確保支援 UTF-8
```bash
# 添加到 shell 配置檔案
export LANG=en_US.UTF-8
export LC_ALL=en_US.UTF-8
export TERM=xterm-256color
```

#### 推薦的終端配置
```json
// WezTerm 配置片段
{
  "font": {
    "normal_family": "JetBrains Mono",
    "size": 12.0
  },
  "color_scheme": "Tokyo Night",
  "enable_tab_bar": true,
  "hide_tab_bar_if_only_one_tab": false
}
```

## 🔍 故障排除

### ❌ 常見安裝問題

#### 問題：`command not found: opencode`
```bash
# 解決方案：重新載入 shell 配置
source ~/.bashrc  # 或 ~/.zshrc, ~/.profile

# 或者重新啟動終端
```

#### 問題：權限拒絕
```bash
# macOS/Linux
sudo chown -R $(whoami) ~/.npm-global

# Windows（以管理員身份運行 PowerShell）
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

#### 問題：網路連接失敗
```bash
# 檢查防火牆設定
# macOS
sudo /usr/libexec/ApplicationFirewall/socketfilterfw --add /usr/local/bin/opencode

# Linux
sudo ufw allow out to any port 443
sudo ufw allow out to any port 80
```

### 🐛 配置問題

#### 問題：API 金鑰無效
```bash
# 檢查金鑰格式
# OpenAI: sk-...
# Anthropic: sk-ant-...
# Google: 通常通過 OAuth 認證

# 重新配置
opencode auth login
# 或在 TUI 中
/connect
```

#### 問題：模型不可用
```bash
# 刷新模型列表
opencode models --refresh

# 檢查提供商狀態
curl -H "Authorization: Bearer YOUR_API_KEY" https://api.openai.com/v1/models
```

## ✅ 安裝完成檢查清單

確認你已完成以下步驟：

- [ ] **✅ 安裝 OpenCode**
  - [ ] 使用推薦的安裝方法
  - [ ] 驗證 `opencode --version` 正常執行

- [ ] **✅ 配置 LLM 提供商**
  - [ ] 選擇並配置至少一個提供商
  - [ ] 測試 API 連接成功
  - [ ] 驗證至少一個模型可用

- [ ] **✅ 系統整合**
  - [ ] 設定必要的環境變數
  - [ ] 配置 shell 別名（可選）
  - [ ] 確認終端顯示正常

- [ ] **✅ 功能測試**
  - [ ] 成功執行 `opencode run "測試訊息"`
  - [ ] TUI 界面正常顯示
  - [ ] 基本功能運行無誤

## 🎉 恭喜！安裝完成！

如果上述檢查清單都完成了，恭喜你！你已經成功：

- 🖥️ 在你的系統上安裝了 OpenCode
- 🔑 配置了 LLM 提供商和 API 金鑰
- ⚙️ 完成了基本的系統整合
- ✅ 驗證了核心功能正常運行

**準備好下一步了嗎？**

👉 **[第一次使用 →](first-time.md)**

---

<div align="center">
  <p><strong>安裝只是開始，精彩的功能還在後頭！</strong></p>
  <p>🔧 遇到問題？查看 <a href="../troubleshooting/common-issues.md">常見問題</a> 或 <a href="https://opencode.ai/discord">Discord 社群</a></p>
</div>