# Insurance Risk Scoring Template

English: Machine Learning Template for Insurance Risk Classification

This repository provides a reusable notebook-based template for building an insurance risk scoring workflow. It is designed for life insurance underwriting and risk classification use cases, where a model helps estimate an applicant's risk level from structured application, demographic, medical, product, and insurance history features.

The project is intended as a practical starting point for:

- InsurTech product managers
- Data science learners
- Insurance analytics teams
- Underwriting automation prototypes
- AI/ML portfolio projects focused on regulated financial services

## Repository Contents

| File | Purpose |
| --- | --- |
| `Insurance_Risk_Scoring_Template.ipynb` | Lightweight reusable notebook template for loading insurance data, preprocessing, training a Random Forest model, evaluating results, and visualizing feature importance. |
| `machine-learning-for-risk-classification-ks.ipynb` | Full case-study notebook based on the Prudential Life Insurance Assessment style workflow, including EDA, preprocessing, feature engineering, model selection, and interpretation. |
| `RESEARCH.md` | Product and market research for the insurance risk-scoring template, following the Vibe Coding workflow. |
| `PRD.md` | Product Requirements Document for the template and future app direction. |
| `TECH_DESIGN.md` | Technical design covering notebook architecture, ML pipeline, future app architecture, storage, and model governance. |
| `AGENTS.md` | AI coding rules for safely modifying this repository. |
| `requirements.txt` | Python dependencies for running the notebooks. |

## Problem Context

Insurance underwriting traditionally requires manual review of applicant information, policy details, health indicators, family history, medical history, and other risk signals. A risk scoring model can support underwriters by:

- Prioritizing applications for review
- Identifying high-risk applicants
- Explaining which features drive risk classification
- Standardizing parts of the underwriting workflow
- Reducing turnaround time for low-complexity cases

This project demonstrates how supervised machine learning can classify insurance applicants into risk levels and surface feature importance for underwriting review.

## Core Workflow

The template follows a practical ML workflow:

1. Load insurance applicant data
2. Inspect data shape, types, missing values, and summary statistics
3. Clean or impute missing values
4. Encode categorical variables
5. Define features and target
6. Split data into training and test sets
7. Scale numeric features
8. Train a classification model
9. Evaluate predictions with confusion matrix and classification report
10. Visualize feature importance

The larger case-study notebook extends this with:

- Exploratory Data Analysis
- Distribution plots
- Correlation heatmaps
- Missing-value analysis
- Train/validation/test split
- Iterative imputation
- K-means feature engineering
- Mutual information feature selection
- VIF multicollinearity analysis
- PCA
- Lasso-based feature selection
- Multiple classifiers and hyperparameter search
- Model interpretation

## Dataset Expectations

The lightweight template expects a CSV file such as:

```text
insurance_data.csv
```

The example target column is:

```text
risk_level
```

You should replace these placeholders with your actual dataset file and target column.

Recommended input feature groups:

- Applicant demographics
- Product information
- Employment or financial information
- Medical history
- Family history
- Insurance history
- Lifestyle or risk indicators
- Prior claims or underwriting decisions, where legally and ethically appropriate

## Quick Start

Clone the repository:

```bash
git clone https://github.com/Robshao/Insurance_risk-scoring_template-.git
cd Insurance_risk-scoring_template-
```

Create and activate a Python environment:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Start Jupyter:

```bash
jupyter lab
```

Open:

```text
Insurance_Risk_Scoring_Template.ipynb
```

Then replace:

```python
df = pd.read_csv('insurance_data.csv')
X = df.drop('risk_level', axis=1)
y = df['risk_level']
```

with your real dataset path and target column.

## Example Use Cases

### Life Insurance Underwriting

Predict applicant risk class based on age, BMI, medical history, family history, product type, and underwriting signals.

### Triage for Manual Review

Separate low-risk applications that may be eligible for straight-through processing from cases requiring human underwriter review.

### Model-Assisted Decision Support

Provide a risk score and feature importance view to help underwriters review cases more consistently.

### InsurTech PM Portfolio Project

Use the notebook as the analytical backbone for a product case study:

- Problem: underwriting is slow and inconsistent
- User: underwriter or underwriting operations lead
- Solution: ML-assisted risk scoring workflow
- Artifact: PRD, metrics framework, risk register, evaluation plan

## Model Evaluation

Minimum recommended evaluation outputs:

- Confusion matrix
- Classification report
- Accuracy
- Precision
- Recall
- F1 score
- Per-class performance
- Feature importance

For insurance use cases, also consider:

- False positive cost
- False negative cost
- High-risk applicant recall
- Underwriter override rate
- Model confidence threshold
- Fairness and bias review
- Data drift monitoring

## Governance and Risk Notes

This template is for learning, prototyping, and portfolio use. It should not be used as an automated underwriting decision system without additional governance.

Production insurance ML systems require:

- Legal and compliance review
- Model risk management
- Bias and fairness testing
- Explainability controls
- Human-in-the-loop review
- Audit logs
- Data privacy controls
- Monitoring for drift and degradation

The model should support underwriter judgment, not replace accountable underwriting decisions in regulated settings.

## Vibe Coding Workflow Files

This repo includes planning documents based on the Vibe Coding workflow:

### `RESEARCH.md`

Defines comparable tools, target users, product opportunity, local-first advantages, and technical challenges.

### `PRD.md`

Defines the MVP scope, user experience requirements, multilingual expectations, model evaluation needs, and technical constraints.

### `TECH_DESIGN.md`

Defines the technical architecture for the notebook workflow and a future offline-first web app version.

### `AGENTS.md`

Defines coding and documentation rules for AI-assisted development in this repository.

## Future Product Direction

The notebook template can evolve into an offline-first insurance risk scoring web app:

- Upload CSV locally
- Configure target column
- Run preprocessing pipeline
- Train baseline model
- Review model metrics
- Explore feature importance
- Save model experiment notes locally
- Export underwriting review reports

Potential frontend stack:

- React
- TypeScript
- Vite
- Tailwind CSS
- Dexie.js / IndexedDB for local experiment storage

Potential ML execution options:

- Python notebook for analysis
- Local Python backend for private experimentation
- WebAssembly / Pyodide for browser-based demos
- Batch export from notebook into static reports

## Project Status

Current state:

- Notebook-first ML template
- No backend
- No deployed app
- No bundled dataset
- Suitable for learning and portfolio development

Recommended next steps:

1. Add a small sample dataset or schema example.
2. Refactor the notebook into reusable pipeline functions.
3. Add model comparison outputs.
4. Add fairness and explainability checks.
5. Add a product-facing PRD for an underwriting copilot or risk review dashboard.

## License and Usage

No license has been specified yet. Add a license before using this project in commercial or public distribution contexts.
