---
layout: about
title: about
permalink: /
subtitle: Quantitative research & mathematical finance · Paris · St. Gallen / HEC

profile:
  align: right
  more_info: >
    <p>Paris, France</p>
    <p><a href="mailto:eliott.elkeslassy@hec.edu">eliott.elkeslassy@hec.edu</a> · +33 6 95 35 97 22</p>
    <p><a href="https://github.com/eelkeslassy">GitHub</a></p>

selected_papers: false
social: true

announcements:
  enabled: false

latest_posts:
  enabled: false
---

<p class="text-muted"><strong>Executive research summary</strong> — quantitative models first; narrative second.</p>

My work sits at the boundary between **stochastic calculus** and **market microstructure**: identifying structures (cointegration, rough volatility, regime dependence), then stress-test it with the frictions that usually destroy backtests—**transaction costs**, partial fills, and explicit **model-risk** budgets.

The arc began in the rigorous formalisms of French Preparatory Classes, then fostered during an exchange in Mathematics at the University of Texas at Austin. This foundation focused on classical dynamics and linear algebra, where the standard was absolute proof and stability analysis; this intuition now governs my approach to Stochastics and Controlled SDEs. The goal is to maintain the mathematical honesty of the hypothesis when passing from discrete hedging to continuous-time limits.

Bridging HEC Paris and the University of St. Gallen (MiQEF), the focus has shifted to the operational reality of Applied Inference. In practice, this means building research systems that survive institutional scrutiny: implementing Engle-Granger cointegration filtering to ensure stationarity before mean reversion, and utilizing Rolling Diagnostics (MAE/MFE, underwater drawdown) to identify regime-dependency. When the data-generating process is non-Markovian—as seen in Limit Order Book microstructure—the objective is to identify the minimal set of statistical assumptions that still admit robust, non-trivial tests.

### Explore

- **[Research overview](/research/)** — themes behind the public labs  
- **[Research proposal](/research/proposal/)** — signatures, Neural SDEs, FEDONets, LOBSTER-scale validation  
- **[Projects](/projects/)** — DeepLOB & Alpha-Gen repositories and quickstarts  
- **[CV](/cv/)** — experience, education, stack  

### Labs

| Lab | Role |
| --- | --- |
| [DeepLOB — Generative Simulator](https://github.com/eelkeslassy/DeepLOB-Generative-Simulator) | Diffusion-style synthetic microstructure; Hurst-type regimes; stylized-fact dashboard. |
| [Alpha-Gen — Research Engine](https://github.com/eelkeslassy/Alpha-Gen) | Multi-strategy vectorized backtests; Johansen / Engle–Granger evidence; Plotly diagnostics. |
