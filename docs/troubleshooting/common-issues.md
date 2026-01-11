# ❓ 常見問題

> OpenCode 使用過程中最常遇到的問題及解決方案！

## 🔌 連接問題

### ❌ API 金鑰無效

**症狀：**
```
Error: Invalid API key provided
```

**解決方案：**
```bash
# 1. 確認金鑰格式正確
echo $OPENAI_API_KEY

# 2. 重新設定金鑰
export OPENAI_API_KEY="sk-proj-xxxx"

# 3. 使用 /connect 重新配置
/connect
```

### ❌ 網路連接逾時

**症狀：**
```
Error: Request timeout after 30000ms
```

**解決方案：**
```bash
# 1. 檢查網路連接
ping api.openai.com

# 2. 配置代理（如需要）
export HTTPS_PROXY="http://proxy:8080"

# 3. 增加逾時時間
# opencode.json
{
  "network": {
    "timeout": 60000
  }
}
```

## 🤖 模型問題

### ❌ 模型不可用

**症狀：**
```
Error: Model 'gpt-5' not found
```

**解決方案：**
```bash
# 查看可用模型
/models

# 切換到有效模型
/model gpt-4o
```

### ❌ 速率限制

**症狀：**
```
Error: Rate limit exceeded
```

**解決方案：**
- 等待幾分鐘後重試
- 升級 API 計劃
- 切換備援模型

## 🔧 工具執行問題

### ❌ 命令執行失敗

**症狀：**
```
Error: Command 'npm' not found
```

**解決方案：**
```bash
# 確認命令存在
which npm

# 設定 PATH
export PATH="$PATH:/usr/local/bin"
```

### ❌ 權限不足

**症狀：**
```
Error: Permission denied
```

**解決方案：**
```bash
# 檢查檔案權限
ls -la target_file

# 修改權限
chmod +x script.sh
```

## 📝 檔案操作問題

### ❌ 檔案找不到

**解決方案：**
```bash
# 使用完整路徑
> 請讀取 /absolute/path/to/file

# 或使用 @file 引用
> 請分析 @src/index.ts
```

### ❌ 編碼問題

**解決方案：**
```json
{
  "file": {
    "defaultEncoding": "utf-8"
  }
}
```

## 🎯 效能問題

### ❌ 回應太慢

**解決方案：**
- 使用更快的模型（如 gpt-4o-mini）
- 減少上下文長度
- 使用本地模型

### ❌ 記憶體不足

**解決方案：**
```bash
# 清除快取
/clear

# 開始新對話
/new
```

---

## 🚀 更多幫助

👉 **[繼續：調試技巧 →](debugging.md)**

---

<div align="center">
  <p><strong>💡 問題解決了嗎？</strong></p>
</div>
