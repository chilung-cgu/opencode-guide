# 🔧 故障排除

> 全面解決 OpenCode 使用過程中可能遇到的問題，讓你無縫使用 AI 開發工具！

## 🔧 故障排除概覽

這裡收集了 OpenCode 使用過程中最常見的問題和詳細解決方案。

### 📋 **問題分類**

```
❌ 安裝問題      - 安裝和配置相關的問題
🔑 連接問題      - LLM 提供商和 API 連接問題
⚙️ 配置問題      - 設定和配置相關問題
🏃 運行問題      - 執行和操作相關問題
🐛 功能異常      - 特定功能的異常行為
📊 性能問題      - 速度和效率相關問題
```

---

## ❌ 安裝問題

### 🎯 **常見安裝錯誤**

#### **問題 1：`command not found: opencode`**
```bash
# 錯誤訊息
zsh: command not found: opencode
```

**原因分析：**
- OpenCode 沒有正確安裝到系統 PATH
- 環境變數沒有正確設置
- 權限問題導致安裝失敗

**解決方案：**

##### **方法一：檢查安裝路徑**
```bash
# 檢查 npm 全域安裝路徑
npm config get prefix

# 檢查該路徑是否在 PATH 中
echo $PATH | grep $(npm config get prefix)

# 如果不在，添加到 PATH
echo 'export PATH="'$(npm config get prefix)/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc  # 或 ~/.zshrc
```

##### **方法二：重新安裝**
```bash
# 卸載舊版本
npm uninstall -g opencode-ai

# 清除 npm 快取
npm cache clean --force

# 重新安裝
npm install -g opencode-ai
```

##### **方法三：使用 npx**
```bash
# 使用 npx 運行（臨時解決方案）
npx opencode-ai

# 添加到 shell alias
echo 'alias opencode="npx opencode-ai"' >> ~/.bashrc
```

#### **問題 2：權限拒絕錯誤**
```bash
# 錯誤訊息
npm ERR! Error: EACCES: permission denied, access '/usr/local/lib/node_modules/opencode-ai'
```

**解決方案：**

##### **使用 nvm 管理 Node.js**
```bash
# 安裝 nvm
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash

# 重新載入 shell
source ~/.bashrc

# 安裝並使用最新 Node.js
nvm install node
nvm use node

# 安裝 OpenCode
npm install -g opencode-ai
```

##### **手動解決權限問題**
```bash
# 創建全域 npm 目錄
mkdir ~/.npm-global

# 配置 npm 使用新目錄
npm config set prefix '~/.npm-global'

# 添加到 PATH
echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.bashrc
source ~/.bashrc

# 重新安裝
npm install -g opencode-ai
```

#### **問題 3：Windows 安裝問題**

##### **PowerShell 執行策略**
```powershell
# 檢查執行策略
Get-ExecutionPolicy

# 如果返回 Restricted，需要修改
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser

# 或者對單個腳本繞過
Set-ExecutionPolicy -ExecutionPolicy Bypass -Scope Process
```

##### **Windows 防火牆問題**
```powershell
# 添加 Windows Defender 例外
Add-MpPreference -ExclusionPath "C:\Users\%USERNAME%\AppData\Roaming\npm"

# 或者臨時禁用實時保護
Set-MpPreference -DisableRealtimeMonitoring $true
```

---

## 🔑 連接問題

### 🌐 **API 連接錯誤**

#### **問題 1：API 金鑰無效**
```bash
# 錯誤訊息
Error: Invalid API key. Please check your API key and try again.
```

**解決方案：**

##### **檢查 API 金鑰格式**
```bash
# OpenAI 格式：sk-xxxxxxxxxxxxx
# Anthropic 格式：sk-ant-xxxxxxxxxxxxx  
# Google 格式：通常通過 OAuth 認證

# 重新配置提供商
opencode
/connect
# 選擇提供商，重新輸入正確的 API 金鑰
```

##### **驗證 API 金鑰有效性**
```bash
# OpenAI 驗證
curl -H "Authorization: Bearer YOUR_API_KEY" https://api.openai.com/v1/models

# Anthropic 驗證
curl -H "x-api-key: YOUR_API_KEY" -H "anthropic-version: 2023-06-01" https://api.anthropic.com/v1/messages

# Google Vertex AI 需要通過 OAuth 2.0 驗證
```

#### **問題 2：網路連接超時**
```bash
# 錯誤訊息
Error: Request timeout. Please check your internet connection.
```

**解決方案：**

##### **檢查網路連接**
```bash
# 測試基本網路連接
ping google.com
ping api.openai.com

# 測試端口連接
telnet api.openai.com 443
# 或使用 nc
nc -zv api.openai.com 443
```

##### **配置代理設置**
```bash
# 如果使用代理，配置環境變數
export HTTP_PROXY=http://proxy.company.com:8080
export HTTPS_PROXY=http://proxy.company.com:8080

# 或者配置 git 代理
git config --global http.proxy http://proxy.company.com:8080
git config --global https.proxy http://proxy.company.com:8080
```

##### **調整超時設定**
```bash
# 在 opencode.json 中配置超時
{
  "provider": {
    "openai": {
      "timeout": 30,
      "max_retries": 3
    }
  }
}
```

#### **問題 3：地區限制問題**

**解決方案：**

##### **使用 VPN**
```bash
# 推薦的 VPN 服務
- ExpressVPN
- NordVPN  
- Surfshark

# 使用 VPN 後重新連接
opencode
/connect
```

##### **使用反向代理**
```bash
# 配置自定義代理
{
  "provider": {
    "custom": {
      "baseURL": "https://your-proxy.com/v1",
      "apiKey": "your-api-key"
    }
  }
}
```

---

## ⚙️ 配置問題

### 🔧 **配置文件錯誤**

#### **問題 1：配置文件格式錯誤**
```bash
# 錯誤訊息
Error: Invalid configuration file. Please check your opencode.json
```

**解決方案：**

##### **驗證 JSON 格式**
```bash
# 檢查 JSON 語法
cat ~/.config/opencode/opencode.json | jq .

# 如果沒有 jq，使用在線驗證器
# https://jsonlint.com/
```

##### **重新生成配置文件**
```bash
# 備份現有配置
cp ~/.config/opencode/opencode.json ~/.config/opencode/opencode.json.backup

# 重置配置
rm ~/.config/opencode/opencode.json
opencode  # 重新生成預設配置
```

#### **問題 2：主題載入失敗**
```bash
# 錯誤訊息
Error: Failed to load theme 'custom-theme'
```

**解決方案：**

##### **檢查主題文件**
```bash
# 檢查主題文件是否存在
ls ~/.config/opencode/themes/custom-theme.json

# 驗證主題格式
cat ~/.config/opencode/themes/custom-theme.json | jq .
```

##### **使用內建主題**
```bash
# 切換到內建主題
/config set theme tokyonight
/config set theme default
```

---

## 🏃 運行問題

### 🎯 **啟動失敗**

#### **問題 1：依賴缺失**
```bash
# 錯誤訊息
Error: Cannot find module 'some-dependency'
```

**解決方案：**

##### **重新安裝依賴**
```bash
# 全域重新安裝
npm install -g opencode-ai

# 清除並重新安裝
npm uninstall -g opencode-ai
npm cache clean --force
npm install -g opencode-ai
```

##### **檢查 Node.js 版本**
```bash
# 檢查 Node.js 版本
node --version

# OpenCode 需要 Node.js >= 16.0.0
# 如果版本太低，升級 Node.js
nvm install 18
nvm use 18
npm install -g opencode-ai
```

#### **問題 2：終端相容性問題**

**解決方案：**

##### **檢查終端支援**
```bash
# 檢查終端類型
echo $TERM

# 檢查顏色支援
echo -e "\033[31mRed\033[0m \033[32mGreen\033[0m"
```

##### **推薦終端**
```bash
# macOS
brew install --cask iterm2
brew install --cask wezterm

# Linux
sudo apt install wezterm
sudo apt install alacritty

# Windows
# 使用 Windows Terminal 或 PowerShell 7+
```

---

## 🐛 功能異常

### 🎨 **界面顯示問題**

#### **問題 1：顏色顯示異常**
```bash
# 問題：終端顯示亂碼或顏色不正確
```

**解決方案：**

##### **配置顏色模式**
```bash
# 在 opencode.json 中配置
{
  "tui": {
    "color_mode": "truecolor"
  }
}
```

##### **檢查終端配置**
```bash
# 設定正確的 TERM 變數
export TERM=xterm-256color
export COLORTERM=truecolor

# 添加到 shell 配置
echo 'export TERM=xterm-256color' >> ~/.bashrc
echo 'export COLORTERM=truecolor' >> ~/.bashrc
```

#### **問題 2：快捷鍵無效**

**解決方案：**

##### **檢查快捷鍵配置**
```bash
# 查看當前快捷鍵
/keybinds show

# 重置快捷鍵
/keybinds reset
```

##### **檢查終端衝突**
```bash
# 某些終端可能攔截快捷鍵
# 嘗試改變 Leader 鍵
/config set keybinds.leader "ctrl+space"
```

---

## 📊 性能問題

### ⚡ **響應緩慢**

#### **問題 1：AI 響應時間長**

**解決方案：**

##### **切換到更快的模型**
```bash
# 切換到 Haiku 模型（最快）
/model claude-3-haiku

# 或使用 mini 模型
/model gpt-4o-mini
```

##### **啟用串流模式**
```bash
# 在配置中啟用串流
{
  "model": {
    "stream": true
  }
}
```

##### **調整上下文大小**
```bash
# 減少上下文長度
/config set max_context_length 4000

# 啟用上下文壓縮
/config set auto_compress_context true
```

#### **問題 2：記憶體使用過高**

**解決方案：**

##### **清理歷史記錄**
```bash
# 清空對話歷史
/clear-history

# 限制歷史大小
/config set history_limit 100
```

##### **調整快取設定**
```bash
# 清理快取
/clear-cache

# 減少快取大小
/config set cache_size 100MB
```

---

## 🔧 調試工具

### 📊 **診斷命令**

#### **全面系統檢查**
```bash
# 運行完整診斷
/doctor

# 輸出示例：
✅ Node.js: 18.17.0 (OK)
✅ npm: 9.6.7 (OK)
✅ OpenCode: 1.0.0 (OK)
✅ Configuration: Valid
❌ Network: Cannot reach api.openai.com
✅ Memory: 45% used
```

#### **日誌檢查**
```bash
# 查看日誌
/logs

# 查看詳細日誌
/logs --verbose

# 導出日誌
/logs export debug.log
```

#### **性能分析**
```bash
# 開始性能分析
/profile start

# 停止分析並查看結果
/profile stop

# 導出分析報告
/profile export performance.json
```

---

## 🎯 預防措施

### ✅ **最佳實踐**

#### **定期維護**
```bash
# 每月執行
1. 更新 OpenCode
   opencode upgrade

2. 清理快取
   /clear-cache

3. 檢查配置
   /doctor

4. 備份配置
   /config export backup.json
```

#### **監控系統狀態**
```bash
# 設定監控
/config set monitoring.enabled true
/config set monitoring.performance true
/config set monitoring.network true
```

---

## 📞 獲取幫助

### 🌐 **社區支援**

#### **Discord 社群**
- **連結**: https://opencode.ai/discord
- **適用**: 實時討論和快速幫助
- **頻道**: #help, #general, #bugs

#### **GitHub Issues**
- **連結**: https://github.com/anomalyco/opencode/issues
- **適用**: 錯誤回報和功能請求
- **格式**: 使用 Issue 模板

#### **Reddit 社群**
- **連結**: https://reddit.com/r/opencode
- **適用**: 經驗分享和問題討論

### 📧 **官方支援**

#### **技術支援**
- **郵箱**: support@opencode.ai
- **回應時間**: 24-48 小時
- **適用**: 企業用戶和嚴重問題

#### **文檔資源**
- **官方文檔**: https://opencode.ai/docs
- **API 文檔**: https://opencode.ai/docs/api
- **更新日誌**: https://opencode.ai/changelog

---

## 🎉 故障排除總結

### ✅ **問題解決策略**

1. **識別問題類型** - 確定是安裝、連接、配置還是運行問題
2. **查看錯誤訊息** - 仔細閱讀並理解錯誤的含義
3. **使用診斷工具** - 利用 `/doctor` 和 `/logs` 進行診斷
4. **嘗試基本解決方案** - 重新安裝、重置配置、重啟系統
5. **尋求社群幫助** - 在 Discord 或 GitHub 上尋求幫助

### 🎯 **預防措施**

1. **定期更新** - 保持 OpenCode 和依賴的最新版本
2. **備份配置** - 定期備份重要的配置文件
3. **監控系統** - 關注系統資源使用情況
4. **學習最佳實踐** - 遵循官方推薦的使用方式

### 🚀 **持續改進**

1. **記錄問題** - 將遇到和解決的問題記錄下來
2. **分享經驗** - 將解決方案分享給社群
3. **參與貢獻** - 改進文檔和幫助其他用戶
4. **關注更新** - 保持對新版本和功能的關注

---

## 🚀 下一步學習

現在 你已經掌握了 OpenCode 的故障排除技巧！

👉 **[繼續：資源中心 →](../resources/downloads.md)**

---

<div align="center">
  <p><strong>恭喜！你已經成為 OpenCode 故障排除的專家！</strong></p>
  <p>💡 訣竅：遇到問題時，冷靜分析，使用診斷工具，善用社群資源</p>
</div>