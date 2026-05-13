# Insurance Risk Scoring Template PRD

English: Product Requirements Document

## 1. 產品概述

Insurance Risk Scoring Template 是一個保險風險分類 notebook 模板，展示如何將保險申請人資料轉換為可訓練的 machine learning pipeline，並輸出風險分類、模型評估與 feature importance。

未來可擴展為 offline-first 的本地 Web app，用於保險風險評分 demo、模型實驗管理與 underwriting workflow prototype。

## 2. 目標使用者

### Primary Users

- InsurTech PM candidate
- Data science learner
- Insurance analytics practitioner
- AI PM portfolio builder

### Secondary Users

- Underwriting operations lead
- Product manager evaluating underwriting automation
- ML engineer building a baseline insurance model

## 3. MVP 功能列表

### Current Notebook MVP

必須包含：

- Load CSV dataset
- Inspect dataset structure
- Clean missing values
- Encode categorical variables
- Define features and target
- Train/test split
- Scale features
- Train baseline classifier
- Evaluate model
- Plot feature importance

### Future Web App MVP

若轉成 React + Dexie.js Web app，MVP 應包含：

- CSV upload
- Dataset preview
- Target column selection
- Feature inclusion/exclusion
- Missing value strategy selection
- Baseline model training
- Metrics dashboard
- Feature importance view
- Experiment notes
- Local experiment history CRUD

## 4. 核心使用流程

### Notebook Flow

```text
Open notebook
  -> Load insurance dataset
  -> Review fields and missing values
  -> Encode and scale features
  -> Train classifier
  -> Evaluate predictions
  -> Interpret feature importance
  -> Document product and model risks
```

### Future App Flow

```text
Upload CSV locally
  -> Select target column
  -> Configure preprocessing
  -> Run baseline model
  -> Review metrics
  -> Save experiment
  -> Export report
```

## 5. 使用者體驗要求

### Notebook UX

- Notebook sections should be clearly numbered.
- Each step should explain why it matters for underwriting.
- Placeholder dataset and target column names must be easy to find and replace.
- Outputs should be suitable for portfolio screenshots.

### Future Web App UX

- Startup should be under 1.5 seconds before loading data.
- CSV upload should not require backend.
- User should understand whether data stays local.
- Evaluation outputs should be legible for PM and non-technical stakeholders.
- High-risk model limitations should be visible, not hidden.

## 6. 多語言支持

Recommended future app languages:

- 繁體中文 `zh-TW`
- English `en-US`

Language requirements:

- Main UI can be Mandarin-first for Robert Shao's AI PM portfolio use.
- Insurance and ML terms should remain English where natural:
  - Underwriting
  - Risk Scoring
  - Feature Importance
  - Confusion Matrix
  - Precision
  - Recall
  - F1 Score
  - Human-in-the-loop
  - Model Governance

## 7. 技術約束

### Current Repo

- Notebook-first
- Python 3
- pandas / numpy / scikit-learn / matplotlib / seaborn
- No backend
- No bundled production dataset

### Future App

- No external backend for MVP
- All uploaded data remains local
- Use Dexie.js / IndexedDB for experiment metadata
- Avoid storing sensitive data in cloud by default
- Use stable unique IDs for experiments

## 8. Data Requirements

Expected dataset characteristics:

- One row per insurance applicant
- Structured tabular features
- A target risk class column
- Numeric and categorical fields
- Missing values may be present

Required user configuration:

- CSV file path
- Target column
- Columns to exclude
- Missing value strategy
- Model type

## 9. Model Requirements

Baseline model:

- Random Forest Classifier

Recommended comparison models:

- Logistic / Softmax Regression
- Gaussian Naive Bayes
- Support Vector Machine
- Decision Tree
- Random Forest
- Gradient Boosting

Minimum evaluation:

- Confusion matrix
- Classification report
- Precision
- Recall
- F1 score
- Feature importance

Insurance-specific evaluation:

- High-risk recall
- False negative review
- Manual override rate
- Class imbalance handling
- Fairness review across sensitive or proxy features

## 10. Governance Requirements

The product must clearly state:

- Risk scores are decision-support, not automatic decisions.
- Human underwriter review is required for regulated production use.
- Model outputs must be auditable.
- Bias and fairness testing is required before production deployment.
- Sensitive applicant data must be protected.

## 11. Success Metrics

### Notebook Success

- A user can replace the dataset path and target column.
- The notebook runs end-to-end on a compatible CSV.
- The user gets model metrics and feature importance.
- The notebook supports portfolio storytelling.

### Future Product Success

- User can upload data locally.
- User can save at least 5 experiment runs.
- Metrics update after each run.
- User can export a report.
- No uploaded data leaves the browser by default.

## 12. Non-goals

Current MVP does not include:

- Production underwriting decisioning
- Cloud deployment
- Real-time API scoring
- Automated compliance approval
- Built-in dataset
- Model registry

Future versions may add these only after governance design.
