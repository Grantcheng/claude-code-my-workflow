---
paths:
  - "Lectures/**/*.tex"
  - "Quarto/**/*.qmd"
  - "api/**/*.py"
  - "models/**/*.py"
  - "notebooks/**/*.ipynb"
  - "scripts/**/*.py"
---

# Quality Gates & Scoring Rubrics

## Thresholds

- **80/100 = Commit** -- good enough to save
- **90/100 = PR** -- ready for deployment
- **95/100 = Excellence** -- aspirational

## Quarto Slides (.qmd)

| Severity | Issue | Deduction |
|----------|-------|-----------|
| Critical | Compilation failure | -100 |
| Critical | Equation overflow | -20 |
| Critical | Broken citation | -15 |
| Critical | Typo in equation | -10 |
| Major | Text overflow | -5 |
| Major | TikZ label overlap | -5 |
| Major | Notation inconsistency | -3 |
| Minor | Font size reduction | -1 per slide |
| Minor | Long lines (>100 chars) | -1 (EXCEPT documented math formulas) |

## R Scripts (.R)

| Severity | Issue | Deduction |
|----------|-------|-----------|
| Critical | Syntax errors | -100 |
| Critical | Domain-specific bugs | -30 |
| Critical | Hardcoded absolute paths | -20 |
| Major | Missing set.seed() | -10 |
| Major | Missing figure generation | -5 |

## Python Scripts (.py)

| Severity | Issue | Deduction |
|----------|-------|-----------|
| Critical | Syntax errors | -100 |
| Critical | Security vulnerabilities (hardcoded secrets, SQL injection) | -50 |
| Critical | Missing error handling for critical paths | -30 |
| Critical | Hardcoded absolute paths | -20 |
| Major | Missing type hints for public functions | -10 |
| Major | No logging/error messages | -10 |
| Major | Inefficient GPU memory usage | -10 |
| Major | Data leakage in time series | -20 |
| Minor | PEP8 style violations | -1 per violation |
| Minor | Missing docstrings | -2 per function |

## FastAPI Endpoints

| Severity | Issue | Deduction |
|----------|-------|-----------|
| Critical | Missing input validation | -30 |
| Critical | No error responses defined | -20 |
| Major | Missing CORS configuration | -10 |
| Major | Inefficient async/await usage | -10 |

## Jupyter Notebooks (.ipynb)

| Severity | Issue | Deduction |
|----------|-------|-----------|
| Critical | Code doesn't run end-to-end | -100 |
| Critical | Missing dependencies | -30 |
| Major | No explanations/markdown | -15 |
| Major | No visualizations for pedagogical notebooks | -10 |
| Minor | Long cells (>50 lines) | -2 per cell |
| Minor | Unclear variable names | -1 per instance |

## Beamer Slides (.tex)

| Severity | Issue | Deduction |
|----------|-------|-----------|
| Critical | XeLaTeX compilation failure | -100 |
| Critical | Undefined citation | -15 |
| Critical | Overfull hbox > 10pt | -10 |

## Enforcement

- **Score < 80:** Block commit. List blocking issues.
- **Score < 90:** Allow commit, warn. List recommendations.
- User can override with justification.

## Quality Reports

Generated **only at merge time**. Use `templates/quality-report.md` for format.
Save to `quality_reports/merges/YYYY-MM-DD_[branch-name].md`.

## Tolerance Thresholds (FinTech Research)

| Quantity | Tolerance | Rationale |
|----------|-----------|-----------|
| VaR estimates | ±1% | Monte Carlo simulation error |
| Sharpe ratio | ±0.05 | Estimation variability |
| Prediction accuracy | ±2% | Model variance across runs |
| GPU memory utilization | ±5% | Hardware variation |
| Backtest returns | ±0.5% | Numerical precision in financial calculations |
| Time series alignment | Exact | No tolerance - must be exact to avoid look-ahead bias |
