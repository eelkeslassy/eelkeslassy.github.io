---
layout: page
title: projects
nav: true
nav_order: 5
permalink: /projects/
description: DeepLOB generative simulator and Alpha-Gen systematic research engine.
---

Open-source **research-grade** implementations you can clone, run, and extend. Both repositories are **Python-first**, designed for transparent experiments rather than black-box “alpha”.

---

## DeepLOB — Generative diffusion for synthetic microstructure

**Repository:** [github.com/eelkeslassy/DeepLOB-Generative-Simulator](https://github.com/eelkeslassy/DeepLOB-Generative-Simulator)

**What it is.** A **diffusion-style generative sandbox** for synthetic market paths with regime knobs (including **rough volatility** via Hurst-type controls and **algorithmic coupling ρ**). The orchestrator coordinates data retrieval, a PyTorch diffusion core, and a **stylized-facts evaluation** suite (Matplotlib dashboard + JSON experiment report).

**Why it exists.** Classical Markovian models often miss the **non-Markovian** structure of high-frequency liquidity and volatility. This lab lets you **stress** hypotheses about coupling and roughness in a reproducible pipeline.

**Outputs (local runs).** `market_dashboard.png`, `experiment_report.json`, and `evaluation_results.png` (ignored from git; regenerate after `pip install -r requirements.txt`).

**Quickstart.**

```bash
git clone https://github.com/eelkeslassy/DeepLOB-Generative-Simulator.git
cd DeepLOB-Generative-Simulator
python3 -m venv .venv && source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -r requirements.txt
python3 research_main.py --coupling 0.2
python3 research_main.py --rough_vol --hurst 0.10 --coupling 0.35
```

---

## Alpha-Gen — Systematic alpha research engine

**Repository:** [github.com/eelkeslassy/Alpha-Gen](https://github.com/eelkeslassy/Alpha-Gen)

**What it is.** A **multi-strategy** research stack with **vectorized backtesting**, **cointegration diagnostics**, and a **four-panel Plotly** report (equity vs benchmark, rolling vol / Sharpe, underwater drawdown, monthly heatmap).

**Strategies (library).**

- **Dual-class arbitrage** — pairs in log prices with Engle–Granger / Johansen / ADF workflow.  
- **Sector pairs** — universe scan + best-evidence pair selection.  
- **Bollinger mean reversion** — classic band touch / mean reversion template.  
- **RL mean reversion (experimental)** — small tabular Q-learning baseline on discretized states (talking point, not production).

**Metrics.** Sharpe, information ratio, Sortino, skew/kurtosis, MAE/MFE on trade runs, beta to benchmark, information coefficient.

**Quickstart.**

```bash
git clone https://github.com/eelkeslassy/Alpha-Gen.git
cd Alpha-Gen
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
python3 run_alpha_report.py \
  '{"strategy":"dual_class_arb","start":"2022-01-01","end":"2024-01-01","asset_a":"GOOG","asset_b":"GOOGL","benchmark":"SPY","lookback":60,"entry_z":2.0,"exit_z":0.5,"transaction_cost_bps":2.0}' \
  ./output/report.html
```

---

## This GitHub Pages site

**Repository:** [github.com/eelkeslassy/eelkeslassy.github.io](https://github.com/eelkeslassy/eelkeslassy.github.io)

Static **Jekyll** site (minimal theme) deployed from `main` via GitHub Pages. Edit Markdown in the repo root; Jekyll rebuilds on push.
