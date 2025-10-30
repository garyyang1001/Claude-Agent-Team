# Claude Sub Agents Workflow - 系統整合指南

## 🎯 整合概述

本指南說明如何將 Claude Sub Agents Workflow 與現有的 Word Weaver AI 系統進行整合，實現無縫的內容創作體驗。

## 🏗️ 系統架構整合

### 現有系統架構
```
Word Weaver AI (主系統)
├── Frontend (React)
│   ├── 用戶界面
│   ├── 內容編輯器
│   └── 設定管理
├── Backend (Node.js)
│   ├── API服務
│   ├── 內容處理
│   └── 數據存儲
└── AI Services
    ├── Gemini API整合
    ├── 去AI味處理
    └── 風格預設系統
```

### 整合後架構
```
Word Weaver AI (擴展版)
├── Frontend (React)
│   ├── 原有功能保持
│   ├── Agents選擇界面
│   ├── 訪談對話界面
│   └── 工作流程監控
├── Backend (Node.js)
│   ├── 原有API保持
│   ├── Agents協調服務
│   ├── 工作流程管理
│   └── 結果整合處理
├── AI Services (原有)
│   ├── Gemini API整合
│   ├── 去AI味處理
│   └── 風格預設系統
└── Claude Sub Agents (新增)
    ├── Orchestrator Layer
    ├── Research Layer
    ├── Interview Layer
    ├── Creation Layer
    └── Optimization Layer
```

## 🔌 API整合規範

### 新增API端點

**1. 工作流程啟動**
```typescript
POST /api/v1/agents-workflow/start
Content-Type: application/json

Request:
{
  "user_input": "我想寫一篇關於時間管理的文章",
  "user_profile": {
    "name": "Gary",
    "background": "數位行銷顧問",
    "goals": ["建立專業權威", "分享實用經驗"],
    "platform": "LinkedIn",
    "style_preference": "professional"
  },
  "content_requirements": {
    "type": "article",
    "length": "medium",
    "target_audience": "專業人士",
    "call_to_action": "諮詢服務"
  }
}

Response:
{
  "session_id": "session_12345",
  "status": "initiated",
  "estimated_time": "25-30 minutes",
  "next_step": "framework_analysis",
  "workflow_id": "workflow_67890"
}
```

**2. 工作流程狀態查詢**
```typescript
GET /api/v1/agents-workflow/status/{session_id}

Response:
{
  "session_id": "session_12345",
  "current_phase": "research",
  "progress": 35,
  "estimated_remaining": "18 minutes",
  "current_agent": "interview_specialist",
  "phase_results": {
    "discovery": {
      "completed": true,
      "selected_framework": "SOLVE",
      "confidence": 0.95
    },
    "research": {
      "completed": false,
      "progress": 60
    }
  }
}
```

**3. 訪談互動**
```typescript
POST /api/v1/agents-workflow/interview
Content-Type: application/json

Request:
{
  "session_id": "session_12345",
  "user_response": "我最大的時間管理挑戰是會議太多，經常被打斷工作..."
}

Response:
{
  "next_question": "能具體描述一下這些會議的類型和頻率嗎？",
  "question_type": "follow_up",
  "progress": 65,
  "estimated_remaining": "5-8 minutes"
}
```

**4. 結果獲取**
```typescript
GET /api/v1/agents-workflow/result/{session_id}

Response:
{
  "session_id": "session_12345",
  "status": "completed",
  "final_content": "...",
  "framework_used": "SOLVE",
  "quality_score": 87,
  "optimization_applied": [...],
  "platform_recommendations": {...},
  "alternative_versions": [...]
}
```

### 與現有功能整合

**1. 風格預設系統整合**
```typescript
// 擴展現有風格預設
interface StylePreset {
  // 原有屬性保持
  name: string;
  template: string;
  category: string;
  
  // 新增屬性
  recommended_framework?: string;
  agent_preferences?: {
    interview_depth: 'shallow' | 'medium' | 'deep';
    optimization_focus: 'quality' | 'engagement' | 'conversion';
    platform_priority: string[];
  };
}
```

**2. 去AI味功能整合**
```typescript
// 在Agents輸出後自動應用去AI味處理
async function processAgentsOutput(content: string, humanizationConfig: HumanizationConfig) {
  // 1. 先執行Agents工作流程
  const agentsResult = await executeAgentsWorkflow(userInput);
  
  // 2. 應用去AI味處理
  const humanizedContent = await humanizeContent(
    agentsResult.final_content, 
    humanizationConfig
  );
  
  // 3. 整合結果
  return {
    ...agentsResult,
    final_content: humanizedContent,
    processing_applied: ['agents_workflow', 'humanization']
  };
}
```

## 💻 Frontend整合

### 新增React組件

**1. AgentsWorkflowButton.tsx**
```typescript
interface AgentsWorkflowButtonProps {
  onStartWorkflow: () => void;
  disabled?: boolean;
}

export const AgentsWorkflowButton: React.FC<AgentsWorkflowButtonProps> = ({
  onStartWorkflow,
  disabled = false
}) => {
  return (
    <button
      onClick={onStartWorkflow}
      disabled={disabled}
      className="agents-workflow-btn"
    >
      <span>🤖 啟動Agents工作流程</span>
      <small>專業化內容創作助手</small>
    </button>
  );
};
```

**2. WorkflowProgressModal.tsx**
```typescript
interface WorkflowProgressModalProps {
  isOpen: boolean;
  sessionId: string;
  onComplete: (result: WorkflowResult) => void;
  onCancel: () => void;
}

export const WorkflowProgressModal: React.FC<WorkflowProgressModalProps> = ({
  isOpen,
  sessionId,
  onComplete,
  onCancel
}) => {
  const [progress, setProgress] = useState<WorkflowProgress | null>(null);
  
  // 定期查詢進度狀態
  useEffect(() => {
    if (isOpen && sessionId) {
      const interval = setInterval(async () => {
        const status = await fetchWorkflowStatus(sessionId);
        setProgress(status);
        
        if (status.status === 'completed') {
          const result = await fetchWorkflowResult(sessionId);
          onComplete(result);
        }
      }, 2000);
      
      return () => clearInterval(interval);
    }
  }, [isOpen, sessionId]);

  return (
    <Modal isOpen={isOpen} onClose={onCancel}>
      <div className="workflow-progress">
        <h3>Agents 工作流程進行中</h3>
        
        {progress && (
          <>
            <ProgressBar value={progress.progress} max={100} />
            <div className="phase-status">
              <span>當前階段：{getPhaseDisplayName(progress.current_phase)}</span>
              <span>預估剩餘：{progress.estimated_remaining}</span>
            </div>
            
            {progress.current_phase === 'research' && (
              <InterviewChat sessionId={sessionId} />
            )}
          </>
        )}
      </div>
    </Modal>
  );
};
```

**3. InterviewChat.tsx**
```typescript
interface InterviewChatProps {
  sessionId: string;
}

export const InterviewChat: React.FC<InterviewChatProps> = ({ sessionId }) => {
  const [messages, setMessages] = useState<ChatMessage[]>([]);
  const [currentInput, setCurrentInput] = useState('');
  const [isLoading, setIsLoading] = useState(false);

  const sendResponse = async () => {
    if (!currentInput.trim()) return;
    
    setIsLoading(true);
    try {
      const response = await submitInterviewResponse(sessionId, currentInput);
      
      setMessages(prev => [
        ...prev,
        { type: 'user', content: currentInput },
        { type: 'agent', content: response.next_question }
      ]);
      
      setCurrentInput('');
    } finally {
      setIsLoading(false);
    }
  };

  return (
    <div className="interview-chat">
      <div className="chat-messages">
        {messages.map((msg, index) => (
          <div key={index} className={`message ${msg.type}`}>
            {msg.content}
          </div>
        ))}
      </div>
      
      <div className="chat-input">
        <textarea
          value={currentInput}
          onChange={(e) => setCurrentInput(e.target.value)}
          placeholder="請分享您的想法..."
          disabled={isLoading}
        />
        <button onClick={sendResponse} disabled={isLoading || !currentInput.trim()}>
          發送
        </button>
      </div>
    </div>
  );
};
```

### 整合到現有界面

**修改 App.tsx**
```typescript
// 新增狀態管理
const [workflowSession, setWorkflowSession] = useState<string | null>(null);
const [showWorkflowModal, setShowWorkflowModal] = useState(false);

// 新增工作流程啟動函數
const startAgentsWorkflow = async () => {
  try {
    const response = await fetch('/api/v1/agents-workflow/start', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        user_input: topic,
        user_profile: {
          // 從現有狀態獲取用戶資料
        },
        content_requirements: {
          // 從現有設定獲取要求
        }
      })
    });
    
    const result = await response.json();
    setWorkflowSession(result.session_id);
    setShowWorkflowModal(true);
  } catch (error) {
    console.error('Failed to start workflow:', error);
  }
};

// 在生成內容區域添加Agents選項
<div className="generation-options">
  <button onClick={generateContent}>
    🔮 標準生成
  </button>
  
  <AgentsWorkflowButton
    onStartWorkflow={startAgentsWorkflow}
    disabled={!topic.trim()}
  />
</div>

// 添加工作流程模態窗口
<WorkflowProgressModal
  isOpen={showWorkflowModal}
  sessionId={workflowSession}
  onComplete={(result) => {
    setGeneratedContent(result.final_content);
    setShowWorkflowModal(false);
    setWorkflowSession(null);
  }}
  onCancel={() => {
    setShowWorkflowModal(false);
    setWorkflowSession(null);
  }}
/>
```

## 🗄️ 數據庫整合

### 新增資料表

**1. workflow_sessions 表**
```sql
CREATE TABLE workflow_sessions (
  id VARCHAR(255) PRIMARY KEY,
  user_id VARCHAR(255),
  status ENUM('initiated', 'in_progress', 'completed', 'failed'),
  selected_framework VARCHAR(50),
  framework_confidence DECIMAL(3,2),
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  completed_at TIMESTAMP NULL,
  total_duration_minutes INT NULL,
  
  -- 用戶輸入數據
  user_input TEXT,
  user_profile JSON,
  content_requirements JSON,
  
  -- 各階段結果
  discovery_results JSON,
  research_results JSON,
  creation_results JSON,
  optimization_results JSON,
  
  -- 最終輸出
  final_content LONGTEXT,
  quality_score INT,
  user_satisfaction_score INT NULL,
  
  INDEX idx_user_id (user_id),
  INDEX idx_status (status),
  INDEX idx_created_at (created_at)
);
```

**2. workflow_interactions 表**
```sql
CREATE TABLE workflow_interactions (
  id INT AUTO_INCREMENT PRIMARY KEY,
  session_id VARCHAR(255),
  agent_name VARCHAR(100),
  interaction_type ENUM('question', 'response', 'analysis', 'result'),
  content TEXT,
  timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  metadata JSON,
  
  FOREIGN KEY (session_id) REFERENCES workflow_sessions(id),
  INDEX idx_session_id (session_id),
  INDEX idx_timestamp (timestamp)
);
```

**3. 擴展現有 generated_content 表**
```sql
ALTER TABLE generated_content ADD COLUMN (
  workflow_session_id VARCHAR(255) NULL,
  generation_method ENUM('standard', 'agents_workflow') DEFAULT 'standard',
  framework_used VARCHAR(50) NULL,
  quality_metrics JSON NULL,
  
  FOREIGN KEY (workflow_session_id) REFERENCES workflow_sessions(id)
);
```

## 🔧 配置管理

### 環境變數新增
```env
# Claude Sub Agents 配置
AGENTS_WORKFLOW_ENABLED=true
AGENTS_API_ENDPOINT=http://localhost:3001
AGENTS_API_KEY=your_agents_api_key

# 工作流程設定
WORKFLOW_DEFAULT_TIMEOUT=1800000  # 30分鐘
WORKFLOW_MAX_SESSIONS_PER_USER=3
WORKFLOW_CLEANUP_INTERVAL=3600000  # 1小時

# Redis配置（用於會話管理）
REDIS_URL=redis://localhost:6379
REDIS_SESSION_TTL=7200  # 2小時
```

### agents-workflow-config.json
```json
{
  "version": "1.0",
  "default_settings": {
    "interview_depth": "medium",
    "optimization_level": "standard", 
    "quality_threshold": 75,
    "timeout_per_phase": {
      "discovery": 300000,
      "research": 720000,
      "creation": 600000,
      "optimization": 480000
    }
  },
  "agent_configurations": {
    "master_workflow": {
      "decision_confidence_threshold": 0.85,
      "fallback_framework": "SOLVE"
    },
    "interview_specialist": {
      "max_questions": 15,
      "min_questions": 8,
      "adaptive_questioning": true
    },
    "optimization_agents": {
      "parallel_execution": true,
      "quality_gate_score": 70
    }
  },
  "platform_integrations": {
    "default_platforms": ["LinkedIn", "Facebook", "Instagram"],
    "customization_enabled": true
  }
}
```

## 🧪 測試整合

### 單元測試
```typescript
// tests/agents-workflow.test.ts
describe('Agents Workflow Integration', () => {
  test('should start workflow with valid input', async () => {
    const response = await request(app)
      .post('/api/v1/agents-workflow/start')
      .send({
        user_input: 'Test content creation',
        user_profile: { name: 'Test User' }
      });
      
    expect(response.status).toBe(200);
    expect(response.body.session_id).toBeDefined();
  });
  
  test('should handle workflow status queries', async () => {
    const sessionId = 'test_session_123';
    
    const response = await request(app)
      .get(`/api/v1/agents-workflow/status/${sessionId}`);
      
    expect(response.status).toBe(200);
    expect(response.body.current_phase).toBeDefined();
  });
});
```

### 端到端測試
```typescript
// e2e/workflow-integration.e2e.ts
describe('Complete Workflow E2E', () => {
  test('should complete entire workflow successfully', async () => {
    // 1. 啟動工作流程
    const startResponse = await startWorkflow({
      user_input: 'Write about productivity tips'
    });
    
    const sessionId = startResponse.session_id;
    
    // 2. 模擬訪談互動
    await simulateInterview(sessionId, [
      'I struggle with time management',
      'I work in marketing',
      'My biggest challenge is meetings'
    ]);
    
    // 3. 等待完成並驗證結果
    const result = await waitForCompletion(sessionId);
    
    expect(result.status).toBe('completed');
    expect(result.final_content).toBeTruthy();
    expect(result.quality_score).toBeGreaterThan(70);
  }, 60000); // 60秒超時
});
```

## 🚀 部署策略

### 分階段部署

**Phase 1: 內部測試 (Week 1)**
- 部署到開發環境
- 內部團隊測試和反饋
- 修正重大問題

**Phase 2: Beta測試 (Week 2-3)**
- 部署到測試環境
- 邀請限量用戶測試
- 收集使用反饋和數據

**Phase 3: 正式發布 (Week 4)**
- 部署到生產環境
- 全面開放功能
- 監控系統穩定性

### 回滾計劃
```javascript
// 功能開關控制
const FEATURE_FLAGS = {
  AGENTS_WORKFLOW_ENABLED: process.env.AGENTS_WORKFLOW_ENABLED === 'true',
  AGENTS_WORKFLOW_BETA: process.env.AGENTS_WORKFLOW_BETA === 'true'
};

// 在關鍵位置添加開關檢查
if (FEATURE_FLAGS.AGENTS_WORKFLOW_ENABLED) {
  // 顯示Agents選項
} else {
  // 隱藏Agents選項，僅顯示標準生成
}
```

## 📊 監控和維護

### 關鍵指標監控
- Agents工作流程啟動率
- 各階段完成時間
- 用戶滿意度評分
- 系統錯誤率和響應時間

### 日誌管理
```typescript
// 結構化日誌格式
interface WorkflowLog {
  timestamp: string;
  session_id: string;
  event_type: 'phase_start' | 'phase_complete' | 'error' | 'user_action';
  agent_name?: string;
  duration_ms?: number;
  metadata: Record<string, any>;
}

// 日誌記錄示例
logger.info('Workflow phase completed', {
  session_id: sessionId,
  event_type: 'phase_complete',
  agent_name: 'interview_specialist',
  duration_ms: 480000,
  metadata: {
    questions_asked: 12,
    response_quality: 'high'
  }
});
```

---

## 📞 技術支援

**開發團隊聯絡：** [dev-team@wordweaver.ai]
**系統管理員：** [sysadmin@wordweaver.ai]
**技術文檔：** [docs.wordweaver.ai/agents-integration]

**最後更新：** 2024-10-30
**文檔版本：** v1.0
**兼容系統：** Word Weaver AI v2.0+