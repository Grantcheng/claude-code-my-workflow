---
paths:
  - "Lectures/**/*.tex"
  - "Quarto/**/*.qmd"
  - "api/**/*.py"
  - "models/**/*.py"
  - "notebooks/**/*.ipynb"
  - "scripts/**/*.py"
---

# FinTech Education Knowledge Base

<!-- Claude reads this before creating/modifying any FinTech content. -->

## Notation Registry

| Rule | Convention | Example | Anti-Pattern |
|------|-----------|---------|-------------|
| Returns | Use $r_t$ for simple returns, $R_t$ for log returns | $r_t = \frac{P_t - P_{t-1}}{P_{t-1}}$ | Mixing notations within same lecture |
| Expected value | Use $\mathbb{E}[\cdot]$ with double brackets | $\mathbb{E}[r_t]$ | Single brackets $E[r_t]$ |
| Variance | Use $\text{Var}(\cdot)$ or $\sigma^2$ | $\sigma^2 = \text{Var}(r_t)$ | "variance of returns" without symbol |
| Volatility | Use $\sigma$ (annualized std dev) | $\sigma = \sqrt{252} \cdot \text{std}(r_t)$ | Using $\nu$ or other symbols |
| Sharpe ratio | Use $\text{SR}$ or $\mathcal{S}$ | $\mathcal{S} = \frac{\mathbb{E}[r_p] - r_f}{\sigma_p}$ | "sharpe" without math notation |
| VaR | Use $\text{VaR}_\alpha$ with confidence level | $\text{VaR}_{0.95} = 2.3\%$ | "VaR = 2.3%" without confidence level |
| Portfolio weights | Use $\mathbf{w}$ (vector), $w_i$ (scalar) | $\mathbf{w} = [w_1, \dots, w_n]^\top$ | Using $x_i$ or $p_i$ inconsistently |
| Feature matrix | Use $\mathbf{X}$ (capital X), features as columns | $\mathbf{X} \in \mathbb{R}^{n \times p}$ | Using lowercase $x$ for matrix |

## Symbol Reference

| Symbol | Meaning | Introduced |
|--------|---------|------------|
| $r_t$ | Simple return at time t | Lecture 2 |
| $R_t$ | Log return at time t | Lecture 2 |
| $\mu$ | Expected return | Lecture 2 |
| $\sigma$ | Volatility (annualized std dev) | Lecture 2 |
| $\mathbf{w}$ | Portfolio weight vector | Lecture 4 |
| $\boldsymbol{\Sigma}$ | Covariance matrix | Lecture 4 |
| $\mathcal{S}$ | Sharpe ratio | Lecture 4 |
| $\text{VaR}_\alpha$ | Value at Risk at confidence level $\alpha$ | Lecture 4 |
| $\text{CVaR}_\alpha$ | Conditional VaR (Expected Shortfall) | Lecture 4 |
| $\mathbf{X}$ | Feature matrix (ML) | Lecture 3 |
| $\mathbf{y}$ | Target vector (ML) | Lecture 3 |
| $\hat{\mathbf{y}}$ | Predicted values | Lecture 3 |
| $\mathcal{L}$ | Loss function | Lecture 3 |
| $f_\theta(\cdot)$ | ML model with parameters $\theta$ | Lecture 3 |

## Lecture Progression

| # | Title | Core Question | Key Notation | Key Method |
|---|-------|--------------|-------------|------------|
| 1 | Introduction to FinTech | How is AI transforming finance? | LLM, RAG, API | Overview of AI applications in finance |
| 2 | Financial Data & APIs | How do we source and prepare financial data? | $r_t, \mu, \sigma$ | Data ingestion, preprocessing, feature engineering |
| 3 | ML for Finance | How can ML predict financial outcomes? | $\mathbf{X}, \mathbf{y}, \mathcal{L}$ | Supervised learning, time series, cross-validation |
| 4 | Risk Modeling | How do we quantify and manage financial risk? | $\mathbf{w}, \boldsymbol{\Sigma}, \text{VaR}$ | Portfolio optimization, VaR/CVaR, Monte Carlo |
| 5 | Algorithmic Trading | How do we design and evaluate trading strategies? | $\alpha, \beta, \mathcal{S}$ | Backtesting, execution, performance attribution |
| 6 | NLP for FinTech | How can LLMs analyze financial text? | BERT, embedding, attention | Sentiment analysis, QA systems, RAG |

## Empirical Applications

| Application | Paper/Resource | Dataset | Lecture(s) | Purpose |
|------------|----------------|---------|------------|---------|
| Portfolio Optimization | Markowitz (1952) | Yahoo Finance, FRED | Lecture 4 | Efficient frontier, risk-return tradeoff |
| VaR Estimation | Jorion (2007) | Historical stock data | Lecture 4 | Risk quantification, regulatory compliance |
| Stock Prediction | Fama & French (1993) | CRSP, Compustat | Lecture 3 | Factor models, ML forecasting |
| Sentiment Trading | Tetlock (2007) | News headlines, 10-K filings | Lecture 6 | NLP for market prediction |
| High-Frequency Trading | Hasbrouck (2007) | Tick data | Lecture 5 | Market microstructure, execution |
| Credit Risk | Merton (1974) | Lending Club data | Lecture 4 | Default prediction, scoring models |

## Design Principles

| Principle | Evidence | Lectures Applied |
|-----------|----------|-----------------|
| **Motivation before formalism** | Students learn faster when they understand "why" first | All lectures start with real-world motivation |
| **Incremental complexity** | Cognitive load theory: build from simple to complex | Lecture 2: returns → log returns → multi-period |
| **Worked examples** | Concrete examples aid transfer learning | Every formula followed by numerical example |
| **Visual-first for complex concepts** | Dual coding theory: images + text improve retention | Lecture 4: efficient frontier diagram before math |
| **Temporal awareness** | Time series require special handling | All ML examples use time-aware cross-validation |
| **Reproducibility** | Science requires replicable results | All code uses `set_seed()` and documented parameters |

## Anti-Patterns (Don't Do This)

| Anti-Pattern | What Happened | Correction |
|-------------|---------------|-----------|
| **Look-ahead bias** | Used future data in training | Use time-aware splits, `TimeSeriesSplit` |
| **Data leakage** | Target variable leaked into features | Drop target before feature engineering |
| **Overfitting** | Complex model with insufficient data | Regularization, cross-validation, simpler models |
| **Ignoring transaction costs** | Backtest ignores trading friction | Include slippage, commissions in evaluation |
| **Non-stationary features** | Used raw prices in regression | Use returns or log prices instead |
| **Survivorship bias** | Dataset only includes surviving firms | Use point-in-time datasets |
| **P-hacking** | Multiple testing without correction | Adjust p-values, use holdout validation |

## Python Code Pitfalls

| Bug | Impact | Fix |
|-----|--------|-----|
| **Hardcoded paths** | Breaks on other machines | Use `Path(__file__).parent` or `here` package |
| **No seed setting** | Results not reproducible | `np.random.seed(20260225)`, `torch.manual_seed(...)` |
| **Ignoring warnings** | Hidden errors accumulate | Use `warnings.filterwarnings('error')` in tests |
| **GPU memory leaks** | CUDA out of memory | Clear cache: `torch.cuda.empty_cache()` |
| **Time zone issues** | Timestamps misaligned | Always use UTC, convert at display time |
| **Divide by zero** | NaN values propagate | Use `np.divide(a, b, out=np.zeros_like(a), where=b!=0)` |
| **Inefficient loops** | Slow execution | Vectorize with NumPy/Pandas, use `.apply()` sparingly |
| **No error handling** | Crashes on edge cases | Try/except with informative messages |
| **Type confusion** | Silent bugs | Use type hints, `mypy` for static checking |

## ML-Specific Pitfalls

| Bug | Impact | Fix |
|-----|--------|-----|
| **Shuffling time series** | Look-ahead bias | Never shuffle, use time-based splits |
| **Scaling before split** | Data leakage | Fit scaler on train only, transform test |
| **Ignoring class imbalance** | Poor minority class performance | Use class weights, SMOTE, or F1-score |
| **No feature importance** | Black box models | SHAP values, permutation importance |
| **Over-reliance on accuracy** | Misleading metrics | Use precision, recall, AUC for finance |

## Tolerance Thresholds

| Quantity | Tolerance | Rationale |
|----------|-----------|-----------|
| VaR estimates | ±1% | Monte Carlo simulation error |
| Sharpe ratio | ±0.05 | Estimation variability |
| Prediction accuracy | ±2% | Model variance across runs |
| GPU memory utilization | ±5% | Hardware variation |
| Backtest returns | ±0.5% | Numerical precision |
| Time series alignment | Exact | No tolerance - must avoid look-ahead bias |
