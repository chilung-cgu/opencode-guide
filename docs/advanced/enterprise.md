# 🏢 企業部署

> 在團隊和企業環境中部署和管理 OpenCode，實現高效協作！

## 🎯 企業部署概覽

OpenCode 提供完整的企業級功能，支援團隊協作、權限管理、審計追蹤等企業需求。無論是小型團隊還是大型組織，都能找到適合的部署方案。

### 🏗️ **部署選項**

```
🏢 企業部署方案
├── 團隊版        (5-50 人團隊)
├── 企業版        (50+ 人組織)
├── 自託管版      (完全控制)
└── 混合部署      (雲端 + 本地)
```

## ⚙️ 團隊配置

### 🎯 **團隊配置文件**

創建團隊共享配置 `.opencode/team.json`：

```json
{
  "$schema": "https://opencode.ai/team-config.json",
  "team": {
    "name": "My Development Team",
    "organization": "My Company"
  },
  "defaults": {
    "model": "anthropic/claude-sonnet-4-5",
    "theme": "company-dark"
  },
  "policies": {
    "requireApproval": true,
    "allowedTools": ["read", "write", "bash"],
    "blockedTools": ["websearch"],
    "maxTokensPerSession": 100000
  }
}
```

### 🎯 **分層配置系統**

```
配置優先級（高 → 低）
├── 用戶配置        ~/.opencode/config.json
├── 專案配置        ./opencode.json
├── 團隊配置        ./.opencode/team.json
└── 組織配置        (從伺服器同步)
```

## 🔐 權限管理

### 🎯 **角色定義**

```json
{
  "roles": {
    "admin": {
      "description": "管理員",
      "permissions": ["*"]
    },
    "developer": {
      "description": "開發者",
      "permissions": [
        "read", "write", "edit",
        "bash:limited",
        "use-agents"
      ]
    },
    "reviewer": {
      "description": "審查者",
      "permissions": [
        "read",
        "use-agents:planning"
      ]
    },
    "viewer": {
      "description": "檢視者",
      "permissions": ["read"]
    }
  }
}
```

### 🎯 **團隊成員配置**

```json
{
  "members": [
    {
      "email": "alice@company.com",
      "role": "admin",
      "groups": ["platform-team"]
    },
    {
      "email": "bob@company.com",
      "role": "developer",
      "groups": ["backend-team", "platform-team"]
    }
  ],
  "groups": {
    "platform-team": {
      "permissions": ["deploy:staging"]
    },
    "backend-team": {
      "permissions": ["database:read"]
    }
  }
}
```

## 🔒 安全配置

### 🎯 **API 金鑰管理**

```json
{
  "security": {
    "apiKeys": {
      "storage": "vault",
      "vaultUrl": "https://vault.company.com",
      "vaultPath": "secret/opencode"
    },
    "rotation": {
      "enabled": true,
      "intervalDays": 90
    }
  }
}
```

### 🎯 **網路安全**

```json
{
  "security": {
    "network": {
      "allowedDomains": [
        "api.openai.com",
        "api.anthropic.com",
        "*.company.com"
      ],
      "blockedDomains": [
        "*.example.com"
      ],
      "proxy": {
        "url": "http://proxy.company.com:8080",
        "auth": "${PROXY_AUTH}"
      }
    }
  }
}
```

### 🎯 **資料保護**

```json
{
  "security": {
    "dataProtection": {
      "sensitivePatterns": [
        "(?i)password\\s*=",
        "(?i)api[_-]?key",
        "sk-[a-zA-Z0-9]+"
      ],
      "action": "mask",
      "logging": {
        "redactSensitive": true,
        "retentionDays": 90
      }
    }
  }
}
```

## 📊 審計與合規

### 🎯 **審計日誌**

```json
{
  "audit": {
    "enabled": true,
    "events": [
      "session.start",
      "session.end",
      "tool.execute",
      "file.write",
      "command.run"
    ],
    "destination": {
      "type": "elasticsearch",
      "url": "https://logs.company.com:9200",
      "index": "opencode-audit"
    }
  }
}
```

### 🎯 **合規報告**

```json
{
  "compliance": {
    "standards": ["SOC2", "GDPR", "HIPAA"],
    "reports": {
      "frequency": "monthly",
      "recipients": ["compliance@company.com"],
      "format": "pdf"
    }
  }
}
```

## 🖥️ 自託管部署

### 🎯 **Docker 部署**

```yaml
# docker-compose.yml
version: '3.8'
services:
  opencode-server:
    image: opencode/server:latest
    ports:
      - "8080:8080"
    environment:
      - DATABASE_URL=postgresql://db:5432/opencode
      - REDIS_URL=redis://redis:6379
      - LICENSE_KEY=${LICENSE_KEY}
    volumes:
      - ./config:/app/config
    depends_on:
      - db
      - redis

  db:
    image: postgres:15
    environment:
      - POSTGRES_DB=opencode
      - POSTGRES_PASSWORD=${DB_PASSWORD}
    volumes:
      - pgdata:/var/lib/postgresql/data

  redis:
    image: redis:7-alpine
    volumes:
      - redisdata:/data

volumes:
  pgdata:
  redisdata:
```

### 🎯 **Kubernetes 部署**

```yaml
# opencode-deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: opencode-server
spec:
  replicas: 3
  selector:
    matchLabels:
      app: opencode
  template:
    metadata:
      labels:
        app: opencode
    spec:
      containers:
      - name: opencode
        image: opencode/server:latest
        ports:
        - containerPort: 8080
        env:
        - name: DATABASE_URL
          valueFrom:
            secretKeyRef:
              name: opencode-secrets
              key: database-url
        resources:
          requests:
            memory: "512Mi"
            cpu: "500m"
          limits:
            memory: "2Gi"
            cpu: "2000m"
```

## 📈 監控與維運

### 🎯 **健康檢查**

```json
{
  "monitoring": {
    "healthCheck": {
      "endpoint": "/health",
      "interval": 30,
      "timeout": 10
    },
    "metrics": {
      "enabled": true,
      "endpoint": "/metrics",
      "format": "prometheus"
    }
  }
}
```

### 🎯 **告警配置**

```json
{
  "alerts": {
    "channels": [
      {
        "type": "slack",
        "webhook": "${SLACK_WEBHOOK}"
      },
      {
        "type": "email",
        "recipients": ["ops@company.com"]
      }
    ],
    "rules": [
      {
        "name": "高 API 延遲",
        "condition": "api_latency_p99 > 5000",
        "severity": "warning"
      },
      {
        "name": "錯誤率過高",
        "condition": "error_rate > 0.05",
        "severity": "critical"
      }
    ]
  }
}
```

## 🔄 備份與災難恢復

### 🎯 **備份策略**

```json
{
  "backup": {
    "enabled": true,
    "schedule": "0 2 * * *",
    "retention": {
      "daily": 7,
      "weekly": 4,
      "monthly": 12
    },
    "destination": {
      "type": "s3",
      "bucket": "opencode-backups",
      "region": "ap-northeast-1"
    }
  }
}
```

---

## 🚀 下一步學習

現在你已經掌握了 OpenCode 的企業部署！

👉 **[返回：進階功能 →](index.md)**

---

<div align="center">
  <p><strong>🏢 企業級部署達成！</strong></p>
  <p>💡 訣竅：從團隊配置開始，逐步添加安全和合規要求</p>
</div>
