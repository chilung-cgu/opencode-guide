# 🔍 調試技巧

> 系統性問題診斷和調試方法！

## 🎯 調試概覽

當遇到問題時，按照系統性的調試流程可以快速定位問題根源。

## 📋 調試清單

### 🎯 **快速診斷**

```bash
# 1. 檢查 OpenCode 版本
opencode --version

# 2. 檢查配置
/config

# 3. 檢查連接狀態
/status

# 4. 查看日誌
/logs
```

## 📝 日誌分析

### 🎯 **啟用詳細日誌**

```json
{
  "logging": {
    "level": "debug",
    "file": "~/.opencode/debug.log"
  }
}
```

### 🎯 **日誌級別**

| 級別 | 說明 | 使用場景 |
|------|------|----------|
| error | 錯誤訊息 | 生產環境 |
| warn | 警告訊息 | 一般使用 |
| info | 資訊訊息 | 追蹤流程 |
| debug | 調試訊息 | 問題排查 |

## 🌐 網路診斷

### 🎯 **測試連接**

```bash
# 測試 API 端點
curl -I https://api.openai.com/v1/models

# 測試代理
curl --proxy http://proxy:8080 https://api.openai.com

# 測試 DNS
nslookup api.anthropic.com
```

### 🎯 **網路問題清單**

- [ ] 防火牆是否阻擋
- [ ] 代理設定是否正確
- [ ] DNS 解析是否正常
- [ ] SSL 憑證是否有效

## 🔧 環境檢查

### 🎯 **環境變數**

```bash
# 檢查所有相關變數
env | grep -E "(OPENAI|ANTHROPIC|OPENCODE)"

# 確認 PATH
echo $PATH
```

### 🎯 **依賴檢查**

```bash
# Node.js 版本
node --version

# npm 版本
npm --version

# Python 版本（如使用）
python3 --version
```

## 🛠️ 重置與恢復

### 🎯 **重置配置**

```bash
# 備份現有配置
cp ~/.opencode/config.json ~/.opencode/config.json.bak

# 重置為預設
opencode --reset-config
```

### 🎯 **清除快取**

```bash
# 清除會話快取
/clear

# 清除所有快取
rm -rf ~/.opencode/cache
```

---

## 🚀 更多幫助

👉 **[繼續：效能優化 →](performance.md)**

---

<div align="center">
  <p><strong>🔍 調試高手！</strong></p>
</div>
