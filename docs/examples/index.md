# 💡 實戰案例

> 通過真實專案案例，學習 OpenCode 在不同開發場景下的最佳實踐應用！

## 🎯 實戰案例概覽

這裡收集了來自真實開發場景的實戰案例，涵蓋不同的技術棧和開發需求。

### 📋 **案例分類**

```
🌐 Web 開發      - 前端技術棧的完整開發流程
🔌 API 開發      - 後端服務和 API 設計實踐
🤖 機器學習      - AI 專案開發和數據科學應用
👥 團隊協作      - 多人協作的開發模式和最佳實踐
```

---

## 🌐 Web 開發案例

### 🎨 **React + TypeScript 全棧應用**

#### **專案背景**
- **目標**：創建一個現代化的任務管理應用
- **技術棧**：React 18, TypeScript, Node.js, PostgreSQL, Tailwind CSS
- **功能需求**：用戶認證、任務管理、實時協作、數據可視化

#### **OpenCode 應用流程**

##### **第一階段：專案初始化**
```bash
# 1. 分析需求和技術選型
opencode --continue
> 請分析這個任務管理應用的需求，推薦合適的技術棧

# AI 分析結果推薦：
# - React 18 for modern frontend
# - TypeScript for type safety  
# - Node.js + Express for backend
# - PostgreSQL for data storage
# - Tailwind CSS for styling

# 2. 創建專案結構
> 請幫我創建完整的專案結構，包含前後端分離架構
```

##### **第二階段：核心功能開發**
```bash
# 3. 創建 React 元件庫
> 請設計可重用的 React 元件系統：
# - TaskCard 元件
# - TaskList 元件  
# - UserAvatar 元件
# - LoginForm 元件

# AI 自動生成完整的 TypeScript 介面和元件實現：
interface TaskProps {
  id: string;
  title: string;
  description?: string;
  status: 'todo' | 'in-progress' | 'completed';
  assignee?: User;
  dueDate?: Date;
  onStatusChange: (id: string, status: Task['status']) => void;
}

export const TaskCard: React.FC<TaskProps> = ({
  id,
  title,
  description,
  status,
  assignee,
  dueDate,
  onStatusChange
}) => {
  // Component implementation
};
```

##### **第三階段：後端 API 開發**
```bash
# 4. 設計和實現 REST API
> 請設計任務管理的 REST API，包含：
# - 用戶認證端點
# - 任務 CRUD 操作
# - 實時通知系統
# - 數據驗證中間件

# AI 生成完整的 Express.js API 實現：
// routes/tasks.ts
import express from 'express';
import { authenticateToken } from '../middleware/auth.js';
import { validateTask } from '../middleware/validation.js';

const router = express.Router();

// GET /api/tasks - 獲取任務列表
router.get('/', authenticateToken, async (req, res) => {
  try {
    const { page = 1, limit = 10, status } = req.query;
    const tasks = await TaskService.getTasks({
      userId: req.user.id,
      page: Number(page),
      limit: Number(limit),
      status: status as TaskStatus
    });
    res.json(tasks);
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});
```

#### **最佳實踐總結**

##### **🎯 OpenCode 使用技巧**
```bash
# 1. 使用 Plan Mode 進行架構設計
<Tab>  # 切換到 Plan Mode
> 請設計這個應用的整體架構，考慮可擴展性和維護性

# 2. 使用專業代理進行代碼審查
@code-reviewer 請審查這個 React 元件的實現
@security-expert 請檢查 API 的安全性

# 3. 使用子代理進行專業化任務
@general 請研究最新的 React 18 最佳實踐
@explore 找出專案中可能存在的性能問題
```

##### **📚 學習重點**
- **類型安全的 React 開發** - TypeScript 與 React 的完美結合
- **現代化 API 設計** - RESTful 原則和實踐
- **組件化架構** - 可重用組件的設計模式
- **實時協作實現** - WebSocket 通信機制

---

## 🔌 API 開發案例

### 🏗️ **微服務架構的電商 API**

#### **專案背景**
- **目標**：設計和實現一個可擴展的電商後端系統
- **技術棧**：Node.js, Express, Docker, Redis, MongoDB, GraphQL
- **服務拆分**：用戶服務、產品服務、訂單服務、支付服務

#### **OpenCode 輔助開發**

##### **服務架構設計**
```bash
# 使用 Plan Mode 進行微服務設計
<Tab>
> 請設計電商系統的微服務架構，考慮：
# - 服務拆分策略
# - 服務間通信機制
# - 數據一致性方案
# - 容錯和監控

# AI 分析並推薦微服務拆分方案
┌─────────────────┐    ┌─────────────────┐
│   用戶服務       │    │   產品服務       │
│ - 認證授權      │    │ - 產品管理      │
│ - 用戶信息       │    │ - 庫存管理      │
│ - 權限控制       │    │ - 分類搜索      │
└─────────────────┘    └─────────────────┘
         │                         │
         │                         │
         └─────────┬───────────────┘
                   │
        ┌─────────────────┐
        │   API Gateway   │
        │ - 路由聚合       │
        │ - 認證中間件     │
        │ - 限流控制       │
        └─────────────────┘
```

##### **核心服務實現**
```bash
# 用戶服務實現
> 請實現用戶服務的核心功能：
# - JWT 認證機制
# - 用戶 CRUD 操作
# - 密碼安全處理
# - 會話管理

# AI 生成的服務實現：
// services/user-service.ts
import jwt from 'jsonwebtoken';
import bcrypt from 'bcrypt';
import { User } from '../models/User.js';

export class UserService {
  static async register(userData: RegisterData): Promise<AuthResponse> {
    // 1. 驗證輸入數據
    // 2. 檢查用戶是否已存在
    // 3. 安全的密碼處理
    // 4. 創建用戶記錄
    // 5. 生成 JWT token
  }

  static async authenticate(credentials: LoginData): Promise<AuthResponse> {
    // 1. 驗證用戶憑證
    // 2. 生成安全的 JWT
    // 3. 更新最後登入時間
    // 4. 返回認證響應
  }
}
```

##### **API 文檔生成**
```bash
# 自動生成 API 文檔
> 請為這個服務生成完整的 API 文檔，包含：
# - OpenAPI 3.0 規範
# - 請求/響應範例
# - 錯誤處理說明
# - 認證機制說明

# AI 生成的 OpenAPI 文檔：
openapi: 3.0.0
info:
  title: 電商 API Gateway
  version: 1.0.0
  description: 微服務架構的電商系統 API

paths:
  /api/v1/auth/register:
    post:
      summary: 用戶註冊
      tags: [Authentication]
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/RegisterData'
      responses:
        201:
          description: 註冊成功
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/AuthResponse'
```

#### **技術挑戰和解決方案**

##### **🔍 分布式事務處理**
```bash
# 研究分布式事務解決方案
@general 請研究電商系統的分布式事務解決方案：
# - Saga 模式
# - 事件驅動架構
# - 補償事務機制

# AI 分析並推薦 Saga 模式實現：
// utils/saga-orchestrator.ts
export class SagaOrchestrator {
  private steps: SagaStep[] = [];
  
  addStep(step: SagaStep): this {
    this.steps.push(step);
    return this;
  }
  
  async execute(transactionData: any): Promise<void> {
    const compensations: (() => Promise<void>)[] = [];
    
    try {
      for (const step of this.steps) {
        const result = await step.execute(transactionData);
        compensations.push(step.compensate.bind(step, result));
      }
    } catch (error) {
      // 執行補償事務
      await this.executeCompensations(compensations);
      throw error;
    }
  }
}
```

##### **📊 性能優化策略**
```bash
# 性能分析和優化
> 請分析這個 API 系統的性能瓶頸：
# - 數據庫查詢優化
# - 快取策略設計
# - 連接池管理
# - API 響應時間優化

# AI 提供的優化建議：
1. **數據庫優化**
   - 使用 Redis 快取熱點數據
   - 實施讀寫分離
   - 添加適當的索引

2. **API 優化**
   - 實施 GraphQL DataLoader
   - 使用連接池
   - 實施響應快取
```

---

## 🤖 機器學習案例

### 🧠 **圖像分類模型的部署服務**

#### **專案背景**
- **目標**：創建一個圖像分類的 Web 服務
- **技術棧**：Python, FastAPI, TensorFlow, Docker, React
- **功能需求**：圖像上傳、分類預測、結果展示、模型管理

#### **OpenCode 輔助開發流程**

##### **模型服務架構設計**
```bash
# 使用 Build Mode 創建完整服務
opencode --model claude-3-5-sonnet
> 請幫我設計一個圖像分類服務的完整架構：
# - FastAPI 後端服務
# - 模型加載和推理優化
# - React 前端界面
# - Docker 容器化部署

# AI 生成的架構設計：
┌─────────────────┐
│   React Frontend│
│ - 圖像上傳界面   │
│ - 結果展示       │
│ - 模型管理       │
└─────────────────┘
         │
         ▼
┌─────────────────┐
│  FastAPI Service│
│ - 圖像處理端點   │
│ - 模型推理       │
│ - 結果返回       │
└─────────────────┘
         │
         ▼
┌─────────────────┐
│ TensorFlow Model │
│ - 圖像分類模型   │
│ - 推理優化       │
│ - 批處理支持     │
└─────────────────┘
```

##### **核心功能實現**
```bash
# FastAPI 服務實現
> 請實現 FastAPI 圖像分類服務：
# - 圖像上傳和驗證
# - 模型加載和推理
# - 結果格式化和返回
# - 異常處理

# AI 生成的服務實現：
// main.py
from fastapi import FastAPI, File, UploadFile, HTTPException
from fastapi.middleware.cors import CORSMiddleware
import tensorflow as tf
import numpy as np
from PIL import Image
import io

app = FastAPI(title="Image Classification Service")

# 跨域中間件
app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],
    allow_methods=["*"],
    allow_headers=["*"],
)

# 全局模型加載
class ModelManager:
    def __init__(self):
        self.model = None
        self.class_names = []
    
    def load_model(self):
        """延遲加載模型"""
        if self.model is None:
            self.model = tf.keras.models.load_model('models/image_classifier.h5')
            with open('models/classes.txt', 'r') as f:
                self.class_names = f.read().splitlines()
    
    def predict(self, image_array: np.ndarray) -> dict:
        """模型預測"""
        self.load_model()
        predictions = self.model.predict(image_array)
        confidence = float(np.max(predictions))
        class_id = int(np.argmax(predictions))
        
        return {
            'class_name': self.class_names[class_id],
            'confidence': confidence,
            'class_id': class_id,
            'all_probabilities': {
                self.class_names[i]: float(prob) 
                for i, prob in enumerate(predictions[0])
            }
        }

model_manager = ModelManager()

@app.post("/predict")
async def predict_image(file: UploadFile = File(...)):
    """圖像分類預測端點"""
    if not file.content_type.startswith('image/'):
        raise HTTPException(status_code=400, detail="File must be an image")
    
    try:
        # 讀取和預處理圖像
        contents = await file.read()
        image = Image.open(io.BytesIO(contents))
        image_array = preprocess_image(image)
        
        # 模型預測
        result = model_manager.predict(image_array)
        
        return {
            "success": True,
            "result": result,
            "filename": file.filename,
            "size": len(contents)
        }
    
    except Exception as e:
        raise HTTPException(status_code=500, detail=str(e))
```

##### **模型優化和部署**
```bash
# 模型優化建議
> 請分析這個 TensorFlow 模型的優化機會：
# - 模型壓縮技術
# - 推理加速
# - 資源使用優化
# - 部署策略改進

# AI 提供的優化方案：
1. **模型壓縮**
   - 量化模型減少體積
   - 剪枝技術減少參數
   - 知識蒸餾保留性能

2. **推理加速**
   - TensorFlow Lite 轉換
   - GPU 加速支持
   - 批處理優化
```

##### **監控和日誌**
```bash
# 實施監控系統
> 請為這個 ML 服務添加監控功能：
# - 模型性能監控
# - 預測質量追蹤
# - 系統資源監控
# - 異常檢測

# AI 生成的監控實現：
// monitoring.py
import time
import psutil
from prometheus_client import Counter, Histogram, Gauge, start_http_server

# Prometheus 指標
REQUEST_COUNT = Counter('requests_total', 'Total requests', ['method', 'endpoint'])
REQUEST_DURATION = Histogram('request_duration_seconds', 'Request duration')
MODEL_INFERENCE_TIME = Histogram('model_inference_seconds', 'Model inference time')
SYSTEM_MEMORY_USAGE = Gauge('system_memory_bytes', 'System memory usage')
CPU_USAGE = Gauge('cpu_usage_percent', 'CPU usage percentage')

class MonitoringMiddleware:
    async def __call__(self, request, call_next):
        start_time = time.time()
        response = await call_next(request)
        
        # 記錄指標
        REQUEST_COUNT.labels(
            method=request.method, 
            endpoint=request.url.path
        ).inc()
        
        REQUEST_DURATION.observe(time.time() - start_time)
        
        # 更新系統指標
        SYSTEM_MEMORY_USAGE.set(psutil.virtual_memory().used)
        CPU_USAGE.set(psutil.cpu_percent())
        
        return response
```

---

## 👥 團隊協作案例

### 🏢 **企業級多服務協作開發**

#### **專案背景**
- **團隊規模**：15人（前端5人、後端7人、DevOps3人）
- **專案複雜度**：微服務架構的企業管理系統
- **協作挑戰**：多團隊協作、代碼規範統一、持續集成

#### **OpenCode 協作最佳實踐**

##### **統一開發環境配置**
```bash
# 創建團隊統一配置
/config export team-config.json
{
  "theme": "tokyonight",
  "model": "anthropic/claude-sonnet-4-5",
  "team_standards": {
    "code_style": "prettier",
    "testing_framework": "jest",
    "documentation": "javadoc"
  },
  "shared_agents": [
    "code-reviewer",
    "security-auditor",
    "api-designer"
  ]
}

# 團隊成員導入配置
/config import team-config.json
```

##### **協作工作流程設計**
```bash
# 設計團隊協作流程
> 請設計15人團隊的高效協作流程：
# - 開發分支管理
# - 代碼審查機制
# - 持續集成流程
# - 文檔維護策略

# AI 推薦的協作工作流程：
1. **分支管理策略**
   - main: 生產環境
   - develop: 開發環境
   - feature/*: 功能開發
   - hotfix/*: 緊急修復

2. **代碼審查流程**
   - 至少2人審查
   - 自動化檢查通過
   - 團隊標準符合
   - 測試覆蓋率 > 80%
```

##### **團隊技能共享**
```bash
# 創建團隊共享技能
/skill create team/frontend-standards
/skill create team/backend-patterns
/skill create team/security-guidelines

# 技能內容範例
---
name: team/frontend-standards
description: 團隊前端開發標準和最佳實踐
audience: [frontend-developers]
---

## 團隊前端標準

### 🎨 **組件設計規範**
- 使用 Atomic Design 原則
- 組件命名採用 PascalCase
- Props 使用 TypeScript 定義
- 必須包含 Storybook 文檔

### 🎯 **狀態管理標準**
- 全局狀態使用 Redux Toolkit
- 組件狀態使用 React Hooks
- API 數據使用 React Query

### 🧪 **測試標準**
- 單元測試：Jest + Testing Library
- 組件測試：Storybook + Chromatic
- E2E 測試：Playwright
```

##### **自動化代碼審查**
```bash
# 設置自動化審查技能
@code-reviewer 請為這個 PR 進行全面審查：
# - 代碼風格一致性
# - 性能影響分析
# - 安全性檢查
# - 測試覆蓋率

# AI 審查結果：
🔍 **代碼審查報告**

## ✅ **通過項目**
- 代碼風格符合團隊標準
- 添加了適當的錯誤處理
- 包含必要的單元測試
- 文檔更新完整

## ⚠️ **需要改進**
- [Performance] 發現潛在的 N+1 查詢問題
- [Security] API 端點缺少輸入驗證
- [Testing] 複雜邏輯缺少邊界條件測試

## 🎯 **建議改進**
1. 添加數據庫查詢優化
2. 實施 API 請求驗證中間件
3. 補充異常場景的測試用例
```

---

## 🎯 實戰案例總結

### ✅ **成功要素**

1. **明確的目標定義** - 每個案例都有清晰的開發目標
2. **合理的技術選型** - 基於需求和團隊技能選擇合適技術
3. **迭代式開發** - 採用敏捷方法逐步完善功能
4. **質量保證** - 貫穿開發流程的測試和審查

### 🎓 **學習重點**

1. **技術整合能力** - 不同技術棧的整合實踐
2. **系統化思維** - 從整體架構考慮問題
3. **協作效率提升** - 團隊協作的最佳實踐
4. **持續改進意識** - 基於反饋不斷優化

### 🚀 **應用建議**

1. **從小規模開始** - 選擇適合團隊規模的實踐方式
2. **重視文檔維護** - 良好的文檔是成功的基礎
3. **建立反饋機制** - 及時收集和處理團隊反饋
4. **持續學習改進** - 跟進技術發展，優化實踐方式

---

## 📚 擴展學習

### 🔍 **深入研究方向**

- **微服務架構模式** - 深入了解服務拆分和通信
- **容器化和編排** - Docker 和 Kubernetes 實踐
- **CI/CD 最佳實踐** - 持續集成和部署流水線
- **監控和日誌系統** - 生產環境的監控和故障排除

### 🌟 **進階技能**

- **系統設計能力** - 大規模系統的架構設計
- **性能優化技巧** - 各種性能瓶頸的解決方案
- **安全防護機制** - 全方位的系統安全保護
- **團隊管理技能** - 技術團隊的管理和領導

---

## 🚀 下一步學習

現在 你已經通過實戰案例掌握了 OpenCode 的實際應用！

👉 **[繼續：故障排除指南 →](../troubleshooting/common-issues.md)**

---

<div align="center">
  <p><strong>恭喜！你已經掌握了 OpenCode 的實戰應用！</strong></p>
  <p>💡 訣竅：從實際項目中學習，將理論轉化為實踐能力</p>
</div>