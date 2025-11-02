# Agents Workflow - Claude Sub Agents 系統
## 使用 Claude Projects 快速建立 17 個 AI 內容創作 Agents

---

## 系統概覽

這是一個完整的多 Agent 內容創作系統,包含 **17 個專業 Agents**,分佈在 **4 個協作層級**,支援 **10 種寫作框架**,目標是為不同個性和需求的用戶提供個性化、高品質的內容創作服務。

### 核心特色

**零編程要求**: 使用 Claude Projects + Custom Instructions,無需任何編程知識
**快速啟動**: 2-3 天即可完成設置和測試
**零額外成本**: 使用現有的 Claude Pro 訂閱即可
**高度客製化**: 17 個專業 Agents 涵蓋各種內容類型
**結構完整**: 4 階段工作流程,從需求分析到品質保證

---

## 文檔導航

### 快速開始

1. **[CLAUDE_PROJECTS_SETUP_GUIDE.md](./CLAUDE_PROJECTS_SETUP_GUIDE.md)**
   - 核心 6 個 Agents 的詳細設置指南
   - 每個 Agent 的 Custom Instructions
   - 測試問題和預期輸出
   - **建議**: 從這裡開始!

### 完整參考

2. **[ALL_17_AGENTS_QUICK_REFERENCE.md](./ALL_17_AGENTS_QUICK_REFERENCE.md)**
   - 所有 17 個 Agents 的 System Prompts
   - 快速參考和設置檢查清單
   - 優先級建議 (P0/P1/P2)
   - **建議**: 作為查詢手冊使用

### 📝 使用手冊

3. **[WORKFLOW_USER_GUIDE.md](./WORKFLOW_USER_GUIDE.md)**
   - 完整的 4 階段工作流程說明
   - 詳細的步驟和輸入模板
   - 完整範例演示
   - 常見問題解答
   - **建議**: 設置完成後必讀!

### 🧪 測試驗證

4. **[TEST_CASES.md](./TEST_CASES.md)**
   - 5 個測試案例 (涵蓋不同框架)
   - 完整的測試腳本和輸入
   - 驗證檢查清單
   - 問題記錄模板
   - **建議**: 用於驗證系統可行性

### 🏗️ 系統設計

5. **[AGENTS_SYSTEM_OVERVIEW.md](./AGENTS_SYSTEM_OVERVIEW.md)**
   - 系統架構和設計理念
   - 17 個 Agents 的詳細說明
   - 工作流程設計
   - 核心創新亮點

6. **[WORKFLOW_COORDINATION_PROTOCOLS.md](./workflow_docs/WORKFLOW_COORDINATION_PROTOCOLS.md)**
   - Agent 間通訊協議
   - 標準化數據格式
   - 錯誤處理機制

7. **[SYSTEM_INTEGRATION_GUIDE.md](./workflow_docs/SYSTEM_INTEGRATION_GUIDE.md)**
   - 與現有系統整合的技術指南
   - API 設計和數據庫結構
   - 前端組件設計

---

## 🗺️ 系統架構

### 4 層協作架構

```
Layer 1: Orchestrator (總指揮層) - 1 Agent
    ↓
Layer 2: Research (研究分析層) - 3 Agents
    ↓
Layer 3: Interview (深度訪談層) - 1 Agent
    ↓
Layer 4: Creation (內容創作層) - 10 Agents
    ↓
Layer 5: Optimization (優化層) - 3 Agents
```

### 17 個專業 Agents

#### 🎭 Orchestrator Layer
1. **Master Workflow Agent** - 總指揮官

#### 🔍 Research Layer
2. **Framework Selector Agent** - 框架選擇專家
3. **Audience Analyzer Agent** - 受眾分析專家
4. **Content Gap Analyst Agent** - 內容缺口分析專家

#### 🎤 Interview Layer
5. **Interview Specialist Agent** - 深度訪談專家

#### 📝 Creation Layer (10 種框架)
6. **LEAD Method Agent** - 邏輯分析型
7. **HEART Method Agent** - 情感故事型
8. **SOLVE Method Agent** - 問題解決型
9. **SPARK Method Agent** - 爭議討論型
10. **TEACH Method Agent** - 教育指導型
11. **STORY Method Agent** - 案例展示型
12. **BUSINESS Method Agent** - B2B專業型
13. **CONVERT Method Agent** - 電商銷售型
14. **PERSONAL Method Agent** - 個人品牌型
15. **ENGAGE Method Agent** - 社群互動型

#### 🔧 Optimization Layer
16. **Content Optimizer Agent** - 內容優化專家
17. **Platform Customizer Agent** - 平台客製化專家
18. **Quality Assurance Agent** - 品質保證專家

---

## 🚀 快速開始 (3 天計劃)

### Day 1: 核心設置 (2-3 小時)

**上午: 設置核心 3 個 Agents**
1. Master Workflow Agent
2. Framework Selector Agent
3. Interview Specialist Agent

**下午: 測試基本流程**
- 運行測試案例 1 的 Phase 1-2
- 驗證需求分析和訪談功能

**預期成果**: ✅ 能夠分析需求、推薦框架、進行訪談

---

### Day 2: 創作功能 (2-3 小時)

**上午: 設置創作 3 個 Agents**
4. SOLVE Method Agent
5. BUSINESS Method Agent
6. HEART Method Agent

**下午: 測試完整流程**
- 運行測試案例 1 的 Phase 3
- 測試內容生成功能

**預期成果**: ✅ 能夠生成完整的框架化內容

---

### Day 3: 優化和驗證 (2-3 小時)

**上午: 設置優化 2 個 Agents**
7. Content Optimizer Agent
8. Quality Assurance Agent

**下午: 完整測試**
- 運行測試案例 1 的 Phase 4
- 測試 2-3 個其他測試案例
- 驗證系統可行性

**預期成果**: ✅ 完成 MVP,系統可正常使用

---

## 💡 使用場景

### 適合誰使用?

✅ **內容創作者**: 部落客、社群媒體創作者、自媒體
✅ **行銷專業人士**: 數位行銷、內容行銷、社群行銷
✅ **創業者**: 需要建立個人品牌和內容行銷
✅ **顧問和專家**: 想分享專業知識和經驗
✅ **企業**: 需要系統化的內容創作流程

### 可以創作什麼?

📝 **專業文章**: 行業洞察、專業分析、教學指南
📖 **個人故事**: 職涯經驗、成長故事、生活感悟
💼 **商業內容**: B2B 案例、產品推廣、服務介紹
📱 **社群內容**: Instagram 貼文、LinkedIn 文章、Blog 文章
🎯 **銷售內容**: Landing Page、廣告文案、電商內容

---

## 📊 系統優勢

### vs. 直接使用 ChatGPT/Claude

| 特性 | 通用 AI | Agents Workflow |
|------|---------|-----------------|
| **專業度** | 一般 | 高(17個專業Agents) |
| **結構化** | 需要自己設計 | 完整4階段流程 |
| **個性化** | 有限 | 10種框架精準匹配 |
| **品質控制** | 需要自己判斷 | 內建QA Agent |
| **一致性** | 不穩定 | 標準化流程 |
| **學習曲線** | 需要prompt工程 | 按流程操作即可 |

### vs. 自動化開發方案

| 特性 | Agents Workflow | Python自動化 | Web應用 |
|------|-----------------|--------------|---------|
| **開發時間** | 2-3天 | 2-3週 | 2-3個月 |
| **技術要求** | 無 | Python開發 | 全棧開發 |
| **初始成本** | $0 | $500-1000 | $10000+ |
| **運營成本** | $20/月 | $50-100/月 | $500+/月 |
| **彈性度** | 極高 | 中 | 需要開發 |
| **適合對象** | 個人用戶 | 小團隊 | 企業產品 |

---

## 🎓 學習路徑

### 新手路徑 (推薦)

1. **閱讀**: [AGENTS_SYSTEM_OVERVIEW.md](./AGENTS_SYSTEM_OVERVIEW.md) (15分鐘)
2. **設置**: 按照 [CLAUDE_PROJECTS_SETUP_GUIDE.md](./CLAUDE_PROJECTS_SETUP_GUIDE.md) 設置核心 6 個 Agents (2小時)
3. **學習**: 閱讀 [WORKFLOW_USER_GUIDE.md](./WORKFLOW_USER_GUIDE.md) (30分鐘)
4. **測試**: 運行 [TEST_CASES.md](./TEST_CASES.md) 中的測試案例 1 (1小時)
5. **實戰**: 用自己的真實案例創作內容 (1-2小時)

### 進階路徑

1. **完整設置**: 設置所有 17 個 Agents (4-6小時)
2. **深度測試**: 測試所有 5 個測試案例 (3-4小時)
3. **優化調整**: 根據使用經驗優化 System Prompts (持續)
4. **擴展應用**: 探索更多使用場景和創新玩法 (持續)

---

## ❓ 常見問題

### Q1: 需要 Claude Pro 訂閱嗎?
**A**: 是的,需要 Claude Pro ($20/月) 才能使用 Projects 功能。

### Q2: 一定要設置所有 17 個 Agents 嗎?
**A**: 不需要!核心 6 個 Agents (MVP) 就能完成基本流程。其他 Agents 可以根據需要逐步添加。

### Q3: 設置需要多長時間?
**A**:
- 核心 6 個 Agents: 2-3 小時
- 完整 17 個 Agents: 6-8 小時

### Q4: 每次創作需要多長時間?
**A**:
- 最小流程: 15-20 分鐘
- 標準流程: 30-40 分鐘
- 完整流程: 45-60 分鐘

### Q5: 生成的內容可以直接發布嗎?
**A**: 建議經過人工審核和潤色。AI 生成的內容是高品質的草稿,但最終需要加入你的個人風格和審核。

### Q6: 如何保證內容品質?
**A**: 系統內建 3 層品質保證:
1. Framework Agent 確保結構完整
2. Content Optimizer 優化品質
3. Quality Assurance Agent 最終檢查

### Q7: 可以用於商業用途嗎?
**A**: 可以!系統設計就是為了商業化內容創作。但請注意:
- 遵守 Anthropic 的使用條款
- 對內容進行最終審核
- 確保內容符合平台規範

### Q8: 如何獲得支持?
**A**:
- 查閱文檔中的常見問題
- 參考測試案例找靈感
- 在 GitHub Issues 提問
- 參與社群討論

---

## 🛠️ 進階擴展

### 未來可能的擴展方向

**短期 (1-3 個月)**:
- [ ] 更多 Framework Agents (如: LIST Method, COMPARISON Method)
- [ ] 多語言支持 (英文、日文等)
- [ ] 內容模板庫

**中期 (3-6 個月)**:
- [ ] Python 自動化腳本
- [ ] Streamlit Web 界面
- [ ] 數據分析和效果追蹤

**長期 (6-12 個月)**:
- [ ] 完整的 Web 應用
- [ ] API 對外服務
- [ ] 多用戶協作功能
- [ ] 商業化產品

---

## 📝 更新日誌

### v1.0 (2025-10-30)
- ✅ 完成 17 個 Agents 定義
- ✅ 完成核心文檔 (設置指南、使用手冊、測試案例)
- ✅ 完成 Claude Projects 實現方案
- ✅ 5 個測試案例和驗證清單

---

## 🤝 貢獻

歡迎貢獻!可以通過以下方式:
- 分享使用經驗和案例
- 提供優化建議
- 報告問題和bug
- 改進文檔
- 開發自動化工具

---

## 📄 授權

本專案採用 MIT License。

---

## 🌟 致謝

感謝所有使用和測試這個系統的朋友!你們的反饋讓系統變得更好。

---

## 📞 聯絡方式

- **專案**: AI Ghost Writer / Agents Workflow
- **GitHub**: [專案連結]
- **Email**: [聯絡信箱]

---

## 🎯 開始使用

準備好開始了嗎?

1. **閱讀**: [AGENTS_SYSTEM_OVERVIEW.md](./AGENTS_SYSTEM_OVERVIEW.md)
2. **設置**: [CLAUDE_PROJECTS_SETUP_GUIDE.md](./CLAUDE_PROJECTS_SETUP_GUIDE.md)
3. **學習**: [WORKFLOW_USER_GUIDE.md](./WORKFLOW_USER_GUIDE.md)
4. **測試**: [TEST_CASES.md](./TEST_CASES.md)
5. **創作**: 用你的真實案例開始創作!

---

**讓 AI 成為你的內容創作夥伴,而不是替代品。** 🚀

---

**製作**: AI Ghost Writer Team
**版本**: 1.0
**最後更新**: 2025-10-30
