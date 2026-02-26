---
paths:
  - "scripts/**/*.py"
  - "notebooks/**/*.ipynb"
  - "models/**/*.py"
  - "explorations/**"
---

# Research Project Orchestrator (Simplified)

**For Python scripts, Jupyter notebooks, and ML experiments** -- use this simplified loop instead of the full multi-agent orchestrator.

## The Simple Loop

```
Plan approved → orchestrator activates
  │
  Step 1: IMPLEMENT — Execute plan steps
  │
  Step 2: VERIFY — Run code, check outputs
  │         Python scripts: python runs without error
  │         Notebooks: nbconvert executes all cells
  │         ML models: training completes, metrics reasonable
  │         GPU code: no CUDA out of memory errors
  │         If verification fails → fix → re-verify
  │
  Step 3: SCORE — Apply quality-gates rubric
  │
  └── Score >= 80?
        YES → Done (commit when user signals)
        NO  → Fix blocking issues, re-verify, re-score
```

**No 5-round loops. No multi-agent reviews. Just: write, test, done.**

## Verification Checklist

- [ ] Script/notebook runs without errors
- [ ] All packages imported at top
- [ ] No hardcoded absolute paths
- [ ] `np.random.seed()` or equivalent set if stochastic
- [ ] Output files created at expected paths
- [ ] GPU memory properly managed (if applicable)
- [ ] No look-ahead bias in time series code
- [ ] Quality score >= 80
