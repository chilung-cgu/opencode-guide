# ⚡ 效能優化

> 提升 OpenCode 性能和回應速度的方法！

## 🎯 效能概覽

優化 OpenCode 的效能可以顯著提升開發體驗，減少等待時間。

## 🚀 模型選擇

### 🎯 **速度 vs 能力**

| 模型 | 速度 | 能力 | 建議場景 |
|------|------|------|----------|
| gpt-4o-mini | ⚡⚡⚡ | ★★★ | 日常開發 |
| claude-haiku | ⚡⚡⚡ | ★★★ | 快速問答 |
| gpt-4o | ⚡⚡ | ★★★★★ | 複雜任務 |
| claude-sonnet | ⚡⚡ | ★★★★★ | 代碼生成 |
| o1 | ⚡ | ★★★★★ | 深度推理 |

### 🎯 **智慧模型切換**

```json
{
  "performance": {
    "autoModelSwitch": true,
    "fastModel": "gpt-4o-mini",
    "powerModel": "claude-sonnet-4-5"
  }
}
```

## 💾 快取優化

### 🎯 **啟用快取**

```json
{
  "cache": {
    "enabled": true,
    "maxSize": "500MB",
    "ttl": 3600
  }
}
```

### 🎯 **快取策略**

- **搜尋結果** - 快取檔案搜尋結果
- **模型回應** - 快取常見問答
- **工具結果** - 快取工具執行結果

## 🌐 網路優化

### 🎯 **代理配置**

```json
{
  "network": {
    "proxy": "http://localhost:7890",
    "timeout": 30000,
    "retries": 3
  }
}
```

### 🎯 **區域選擇**

使用最近的 API 端點可減少延遲。

## 📊 監控效能

### 🎯 **效能指標**

```bash
# 查看效能統計
/stats

# 輸出
📊 效能統計
├── 平均回應時間: 1.2s
├── 快取命中率: 85%
├── Token 使用量: 15,000/天
└── 錯誤率: 0.1%
```

## 🔋 資源管理

### 🎯 **記憶體優化**

```json
{
  "memory": {
    "maxContextSize": 50000,
    "pruneOnLimit": true
  }
}
```

---

## 🚀 更多幫助

👉 **[返回：故障排除 →](index.md)**

---

<div align="center">
  <p><strong>⚡ 效能達人！</strong></p>
</div>
