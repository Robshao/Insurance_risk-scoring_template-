# AGENTS.md

This repository contains an insurance risk scoring machine learning template.

## Project Context

The project demonstrates how to classify insurance applicants by risk level using structured insurance application data.

Current form:

- Notebook-first
- Python 3
- pandas / numpy / scikit-learn
- No backend
- No production dataset

Future direction:

- Reusable ML pipeline
- InsurTech AI PM portfolio project
- Possible offline-first React + Dexie.js web app

## Modification Rules

### Scope Control

When editing, keep changes scoped.

Examples:

- If asked to update docs, do not modify notebooks.
- If asked to refactor preprocessing, do not change model evaluation.
- If asked to add a future app plan, do not scaffold an app unless explicitly requested.

### Data Safety

Never commit:

- Real applicant PII
- Health data
- Financial data
- Raw proprietary insurance datasets
- API keys or credentials

Use placeholder filenames such as:

```text
insurance_data.csv
```

### Notebook Rules

When modifying notebooks:

- Preserve section order unless the task asks for restructuring.
- Keep explanatory markdown near code cells.
- Make dataset path and target column easy to change.
- Avoid hidden assumptions about column names.
- Add comments only when they clarify non-obvious ML or insurance logic.

### Python Style

Use:

- Clear function names
- Reproducible random seeds
- Explicit train/test split
- Metrics beyond accuracy
- Stable dependency names in `requirements.txt`

Prefer:

- Small reusable functions
- Explicit model configs
- Clear markdown explanations

Avoid:

- Hardcoded local absolute paths
- Unexplained feature drops
- Silent data leakage
- Treating model output as final underwriting decision

## ML Governance Rules

Insurance risk scoring is a regulated-domain use case. Any model documentation must mention:

- Human-in-the-loop review
- Bias and fairness testing
- Explainability
- Auditability
- Model drift
- Data privacy

Do not frame this template as production-ready automated underwriting.

Use language like:

```text
decision support
underwriter review
prototype
portfolio demo
baseline model
```

Avoid language like:

```text
fully automated approval
production underwriting engine
guaranteed risk prediction
```

## Future Web App Rules

If this repo evolves into a React app:

- UI components must not directly access storage.
- Use Service / Repository layers.
- Use Dexie.js / IndexedDB for local experiment persistence.
- Keep uploaded data local by default.
- Use stable unique IDs, not array indexes.
- Support `zh-TW` and `en-US` if multilingual UI is added.

Recommended flow:

```text
UI Component -> Hook / Service -> Repository -> Dexie.js / IndexedDB
```

## Validation

For documentation-only changes:

- Check links and filenames.
- Ensure README accurately reflects repo contents.

For notebook changes:

- Run notebook top-to-bottom if data is available.
- Verify imports work.
- Verify target column exists.
- Verify model metrics render.

For future app changes:

- Run lint/build.
- Verify local persistence survives reload.

## Git Rules

- Commit focused changes with clear messages.
- Do not rewrite history unless explicitly requested.
- Do not force push unless explicitly requested.
