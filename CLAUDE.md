# CLAUDE.MD -- Academic Project Development with Claude Code

<!-- HOW TO USE: Replace [BRACKETED PLACEHOLDERS] with your project info.
     Customize Beamer environments and CSS classes for your theme.
     Keep this file under ~150 lines — Claude loads it every session.
     See the guide at docs/workflow-guide.html for full documentation. -->

**Project:** AI-Powered FinTech Education & Research Assistant
**Institution:** University FinTech Programs
**Branch:** main

---

## Core Principles

- **Plan first** -- enter plan mode before non-trivial tasks; save plans to `quality_reports/plans/`
- **Verify after** -- compile/render and confirm output at the end of every task
- **Single source of truth** -- Beamer `.tex` is authoritative; Quarto `.qmd` derives from it
- **Quality gates** -- nothing ships below 80/100
- **[LEARN] tags** -- when corrected, save `[LEARN:category] wrong → right` to MEMORY.md

---

## Folder Structure

```
[FINTECH-PROJECT]/
├── CLAUDE.MD                    # This file
├── .claude/                     # Rules, skills, agents, hooks
├── Bibliography_base.bib        # Centralized bibliography
├── Figures/                     # Figures and images
├── Preambles/header.tex         # LaTeX headers
├── Lectures/                    # Beamer .tex files
├── Quarto/                      # RevealJS .qmd files + theme
├── docs/                        # GitHub Pages (auto-generated)
├── scripts/                     # Utility scripts
├── api/                         # FastAPI backend
├── models/                      # ML models & training scripts
├── data/                        # Datasets & preprocessing
├── notebooks/                   # Jupyter notebooks
├── vector_db/                   # Vector database indices
├── quality_reports/             # Plans, session logs, merge reports
├── explorations/                # Research sandbox (see rules)
├── templates/                   # Session log, quality report templates
└── master_supporting_docs/      # Papers and existing slides
```

---

## Commands

```bash
# LaTeX (3-pass, XeLaTeX only)
cd Lectures && TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode file.tex
BIBINPUTS=..:$BIBINPUTS bibtex file
TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode file.tex
TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode file.tex

# Deploy Quarto to GitHub Pages
./scripts/sync_to_docs.sh LectureN

# Run FastAPI backend
uvicorn api.main:app --reload --host 0.0.0.0 --port 8000

# Quality score
python scripts/quality_score.py Quarto/file.qmd
python scripts/quality_score.py api/*.py
python scripts/quality_score.py models/*.py
```

---

## Quality Thresholds

| Score | Gate | Meaning |
|-------|------|---------|
| 80 | Commit | Good enough to save |
| 90 | PR | Ready for deployment |
| 95 | Excellence | Aspirational |

---

## Skills Quick Reference

| Command | What It Does |
|---------|-------------|
| `/compile-latex [file]` | 3-pass XeLaTeX + bibtex |
| `/deploy [LectureN]` | Render Quarto + sync to docs/ |
| `/extract-tikz [LectureN]` | TikZ → PDF → SVG |
| `/proofread [file]` | Grammar/typo/overflow review |
| `/visual-audit [file]` | Slide layout audit |
| `/pedagogy-review [file]` | Narrative, notation, pacing review |
| `/qa-quarto [LectureN]` | Adversarial Quarto vs Beamer QA |
| `/slide-excellence [file]` | Combined multi-agent review |
| `/translate-to-quarto [file]` | Beamer → Quarto translation |
| `/validate-bib` | Cross-reference citations |
| `/devils-advocate` | Challenge slide design |
| `/create-lecture` | Full lecture creation |
| `/commit [msg]` | Stage, commit, PR, merge |
| `/lit-review [topic]` | Literature search + synthesis |
| `/research-ideation [topic]` | Research questions + strategies |
| `/interview-me [topic]` | Interactive research interview |
| `/review-paper [file]` | Manuscript review |
| `/data-analysis [dataset]` | End-to-end Python analysis |
| `/deploy-api` | Deploy FastAPI backend to GPU |
| `/validate-backtest` | Check backtesting for look-ahead bias |
| `/optimize-gpu` | Optimize GPU kernel performance |

---

<!-- CUSTOMIZE: Replace the example entries below with your own
     Beamer environments and Quarto CSS classes for FinTech slides. -->

## Beamer Custom Environments

| Environment       | Effect        | Use Case       |
|-------------------|---------------|----------------|
| `keybox` | Gold background box | Key FinTech concepts |
| `highlightbox` | Gold left-accent box | Important takeaways |
| `riskbox[Title]` | Red-bordered titled box | Risk warnings and caveats |
| `mathbox` | Blue-background math box | Financial formulas and derivations |
| `codebox` | Monospace font box | Python code snippets |

<!-- Examples:
| `keybox` | Gold background box | Key FinTech concepts |
| `highlightbox` | Gold left-accent box | Important takeaways |
| `definitionbox[Title]` | Blue-bordered titled box | Formal definitions |
-->

## Quarto CSS Classes

| Class              | Effect        | Use Case       |
|--------------------|---------------|----------------|
| `.smaller` | 85% font | Dense content slides |
| `.positive` | Green bold | Positive financial outcomes |
| `.negative` | Red bold | Risk warnings, losses |
| `.tech` | Blue monospace | Technical terms, code |
| `.formula` | Display math style | Financial formulas |

---

## Current Project State

| Lecture | Beamer | Quarto | Key Content |
|---------|--------|--------|-------------|
| 1: Introduction to FinTech | `Lecture01_Intro.tex` | `Lecture1_Intro.qmd` | AI in finance, course overview, LLM applications |
| 2: Financial Data & APIs | `Lecture02_Data.tex` | `Lecture2_Data.qmd` | Data sources, preprocessing, feature engineering |
| 3: ML for Finance | `Lecture03_ML.tex` | `Lecture3_ML.qmd` | Supervised learning, time series, backtesting |
| 4: Risk Modeling | `Lecture04_Risk.tex` | `Lecture4_Risk.qmd` | VaR, CVaR, portfolio optimization |
| 5: Algorithmic Trading | `Lecture05_Trading.tex` | `Lecture5_Trading.qmd` | Trading strategies, execution, evaluation |
| 6: NLP for FinTech | `Lecture06_NLP.tex` | `Lecture6_NLP.qmd` | Sentiment analysis, LLM RAG, financial QA |
