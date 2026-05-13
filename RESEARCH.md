# Insurance Risk Scoring Template：需求研究

English: Research for Insurance Risk Scoring Template

## 1. 項目目標

本項目是一個 notebook-first 的保險風險評分模板，用於展示如何使用機器學習對保險申請人進行風險分類。

核心用途：

- 幫助理解 underwriting risk classification
- 建立可重用的 ML pipeline
- 支援 InsurTech / FinTech / AI PM portfolio case study
- 為未來的離線優先風險評分 Web app 打基礎

## 2. 同類產品與參考方向

### Underwriting Workbench

常見功能：

- 申請人資料匯入
- 風險規則檢查
- 風險分數或等級
- 人工核保任務分派
- 審批記錄與 audit trail

啟發：

- ML 模型不應只輸出預測結果，也需要提供可解釋信號。
- 高風險案例應進入 Human-in-the-loop review。
- 產品應追蹤 underwriter override，作為模型改善依據。

### Credit Risk Scoring Tools

常見功能：

- 特徵工程
- 分數卡模型
- 分群與風險等級
- 模型性能監控
- 合規與公平性報告

啟發：

- 保險風險評分也需要 model governance。
- 分數本身不是決策，應配合 policy rules 和人工審核。
- 需要關注 false positive / false negative 的業務成本。

### Kaggle-style ML Notebooks

常見功能：

- Exploratory Data Analysis
- Missing value handling
- Feature engineering
- Model training
- Model comparison
- Metrics visualization

啟發：

- Notebook 適合展示推理過程與 portfolio storytelling。
- 若要轉成產品，需要把探索性程式拆成 pipeline、service、UI。

### AI-native InsurTech Products

常見功能：

- AI underwriting assistant
- Document extraction
- Application risk summary
- Explainable recommendation
- Case prioritization

啟發：

- 風險評分模型可以成為 AI underwriting copilot 的核心能力之一。
- PM 需要把模型指標轉成 business metrics，例如 review time、approval quality、loss ratio proxy。

## 3. 目標使用者

### Data Science Learner

需求：

- 學習完整 ML classification pipeline
- 理解保險資料的 EDA 和 preprocessing
- 建立 portfolio notebook

### InsurTech Product Manager

需求：

- 理解 underwriting automation 的產品邏輯
- 能把模型能力轉成 PRD 和 metrics
- 能回答 AI PM 面試中的 risk and compliance 問題

### Underwriting Analytics Team

需求：

- 快速建立 baseline model
- 比較不同特徵和模型
- 初步理解可解釋性與模型風險

## 4. 為什麼離線優先與本地存儲有價值

如果本模板未來演進成 Web app，離線優先會非常重要。

### 資料敏感性

保險申請資料可能包含個人健康、家庭、財務、生活方式與身份資訊。即使是 demo，也應避免預設上傳到外部後端。

Local-first 優勢：

- 原始 CSV 留在本機
- 實驗結果保存在本地 IndexedDB
- 降低 PII 外洩風險
- 更適合 regulated domain prototype

### 快速實驗

PM 或分析師可能需要多次調整特徵、target column、模型和 evaluation threshold。

Local-first 優勢：

- 不需要登入
- 不需要配置後端
- 可快速比較 experiment runs
- 可離線做模型 demo

### Portfolio 使用

對作品集而言，local-first app 可以讓使用者展示產品和模型流程，而不暴露真實敏感資料。

## 5. IndexedDB / Dexie.js 技術挑戰

### 挑戰 1：大型資料集儲存與查詢

保險 CSV 可能有上萬行與上百個欄位。IndexedDB 可以存資料，但需要謹慎設計 schema 和索引。

應對：

- 原始資料與實驗結果分表
- 避免一次性把所有資料渲染到 UI
- 使用 pagination 和 sampling

### 挑戰 2：模型實驗版本管理

同一份資料可能產生多個 experiment runs。每次 run 都有模型、特徵、metrics、timestamp 和 notes。

應對：

- 建立 `experiments` table
- 保存 config、metrics、feature list、artifact refs
- 使用 stable IDs 而不是 array index

### 挑戰 3：瀏覽器端 ML 性能限制

如果使用 Pyodide、WASM 或 JavaScript ML libraries，訓練大型模型可能卡住 UI。

應對：

- 使用 Web Worker
- 將重計算任務放到 background thread
- 對 demo 使用 sampling 或 baseline model

## 6. 產品機會結論

本 repo 的價值不只是 notebook，而是可以成為 InsurTech AI PM portfolio 的完整案例：

- Problem：核保慢、人工判斷不一致
- User：underwriter / underwriting operations lead
- Model：risk classification baseline
- Product：AI-assisted risk review workflow
- Metrics：decision time、model recall、override rate、compliance review rate
- Governance：explainability、fairness、audit trail、Human-in-the-loop

這使它能同時服務 data science learning 和 AI PM interview storytelling。
