# Insurance Risk Scoring Template：技術設計

English: Technical Design

## 1. Current Architecture

The repository is currently notebook-first.

Files:

- `Insurance_Risk_Scoring_Template.ipynb`
- `machine-learning-for-risk-classification-ks.ipynb`

The lightweight template uses:

- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn

Core model:

- RandomForestClassifier

Core outputs:

- Confusion matrix
- Classification report
- Feature importance chart

## 2. Notebook Pipeline

```text
CSV Dataset
  -> pandas DataFrame
  -> EDA
  -> missing value handling
  -> categorical encoding
  -> feature / target split
  -> train / test split
  -> scaling
  -> model training
  -> prediction
  -> evaluation
  -> feature importance visualization
```

## 3. Recommended Notebook Refactor

To make the template more reusable, split repeated logic into functions:

```python
def load_dataset(path: str) -> pd.DataFrame:
    return pd.read_csv(path)

def encode_categorical_columns(df: pd.DataFrame) -> pd.DataFrame:
    encoded = df.copy()
    categorical_cols = encoded.select_dtypes(include=["object"]).columns
    for col in categorical_cols:
        encoded[col] = LabelEncoder().fit_transform(encoded[col].astype(str))
    return encoded

def train_baseline_model(X_train, y_train) -> RandomForestClassifier:
    model = RandomForestClassifier(n_estimators=100, random_state=42)
    model.fit(X_train, y_train)
    return model
```

Recommended folder structure if converting from notebook-only to package-style:

```text
notebooks/
  Insurance_Risk_Scoring_Template.ipynb
  machine-learning-for-risk-classification-ks.ipynb
src/
  data_loading.py
  preprocessing.py
  modeling.py
  evaluation.py
  visualization.py
tests/
  test_preprocessing.py
requirements.txt
README.md
```

## 4. Future Offline-first Web App Architecture

If this becomes a React + Dexie.js product, use:

```text
UI Component -> Hook / Service -> Repository -> Dexie.js / IndexedDB
```

Suggested stack:

- React
- TypeScript
- Vite
- Tailwind CSS
- Dexie.js
- Web Worker for heavy local processing

## 5. Future Dexie.js Schema

```ts
export interface DatasetRecord {
  id: string;
  name: string;
  rowCount: number;
  columnCount: number;
  targetColumn: string;
  createdAt: string;
  updatedAt: string;
}

export interface ExperimentRecord {
  id: string;
  datasetId: string;
  modelType: string;
  targetColumn: string;
  featureColumns: string[];
  preprocessingConfig: {
    missingValueStrategy: string;
    scaling: string;
    encoding: string;
  };
  metrics: {
    accuracy?: number;
    precisionMacro?: number;
    recallMacro?: number;
    f1Macro?: number;
  };
  notes: string;
  createdAt: string;
}

export interface FeatureImportanceRecord {
  id: string;
  experimentId: string;
  featureName: string;
  importance: number;
}
```

Dexie stores:

```ts
this.version(1).stores({
  datasets: 'id, name, targetColumn, createdAt, updatedAt',
  experiments: 'id, datasetId, modelType, targetColumn, createdAt',
  featureImportances: 'id, experimentId, featureName, importance',
});
```

## 6. State Management

Notebook:

- State is held in notebook variables.

Future app:

- React state for UI controls
- Dexie.js for persistent experiment metadata
- Web Worker state for long-running preprocessing/training
- Service layer for derived metrics

Avoid:

- UI components directly writing to IndexedDB
- Storing large datasets in React global state
- Blocking the main thread during large CSV parsing

## 7. Performance Design

### Notebook

- Use sampling for expensive visualizations
- Avoid rendering hundreds of plots by default
- Cache intermediate preprocessing outputs where useful

### Future Browser App

- Parse CSV in a Web Worker
- Store experiment metadata in Dexie.js
- Use row sampling for preview
- Paginate data table views
- Keep model training lightweight for browser demos

## 8. Model Governance Design

Insurance ML is a regulated-domain use case. Any production version must include:

- Human-in-the-loop review
- Explainability output
- Audit trail
- Bias/fairness testing
- Model drift monitoring
- Versioned model experiments
- Data privacy controls

Recommended model cards:

```text
Model purpose
Training data source
Target variable
Feature groups
Known limitations
Evaluation metrics
Fairness review
Human review policy
Monitoring plan
```

## 9. Validation Strategy

Notebook validation:

- Confirm the notebook runs from top to bottom with a compatible dataset.
- Confirm target column exists.
- Confirm no missing target values.
- Confirm encoded features are numeric before model training.
- Confirm train/test split preserves target distribution where possible.

Model validation:

- Confusion matrix
- Per-class precision and recall
- Macro F1
- High-risk recall
- Error analysis by class

Future app validation:

- Upload CSV locally
- Save experiment to IndexedDB
- Reload page and verify experiment persists
- Delete experiment and verify removal
- Run large CSV sample without UI freeze

## 10. Security and Privacy

Current repo:

- Do not commit real applicant data.
- Do not commit PII.
- Keep datasets outside git unless anonymized and licensed.

Future app:

- Data stays local by default.
- No backend upload without explicit user action.
- Export should clearly indicate what is included.
- Consider redaction for sample reports.

## 11. Deployment

Current notebook:

- Can be run locally in Jupyter.
- Can be viewed on GitHub.
- Can be run in Colab with dataset upload if adapted.

Future app:

- Vite static build can deploy to Vercel.
- No environment variables required for local-only MVP.

Vercel settings:

- Build command: `npm run build`
- Output directory: `dist`
- Install command: `npm install`
