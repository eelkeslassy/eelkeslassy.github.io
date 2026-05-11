---
layout: page
title: research
nav: true
nav_order: 3
permalink: /research/
description: Non-Markovian microstructure, systematic signals under frictions, and reproducible evaluation.
---

This page collects the **research through-line** behind the public repositories: non-Markovian microstructure, systematic signals under frictions, and reproducible evaluation.

**Full programme:** read **[Research proposal: Signature-based generative SDEs](/research/proposal/)** (Neural SDEs, path signatures, FEDONets, LOBSTER-scale validation).

## Non-Markovian LOB dynamics & rough volatility

Electronic limit order books exhibit **path dependence**, **volatility clustering**, and **heavy tails** that are poorly approximated by Markovian diffusions with constant volatility. A productive modeling stance is to treat volatility as a **rough** process (Hurst exponent **H < ½**) and to study how **algorithmic coupling** (**ρ**) concentrates liquidity risk during stress.

The [DeepLOB simulator](https://github.com/eelkeslassy/DeepLOB-Generative-Simulator) is a **controlled laboratory**: toggle rough-volatility regimes and coupling, generate synthetic paths, and compare distributional signatures to empirical benchmarks (stylized facts, ACF structure, tail behavior).

## Systematic signals & cointegration discipline

Mean-reversion on spreads without a **cointegration** argument is fragile. The workflow I implement is deliberately conservative:

- **Engle–Granger** and **Johansen** evidence on log prices  
- **ADF** on residuals where appropriate  
- **Rolling z-scores** with **entry/exit hysteresis**  
- **Transaction costs** applied via turnover, plus optional **stop / take-profit** controls  

The [Alpha-Gen engine](https://github.com/eelkeslassy/Alpha-Gen) packages this into a **vectorized backtester** with benchmark-relative metrics (information ratio, tracking error, beta), tail diagnostics (skew, kurtosis), drawdown paths, and **information coefficient** (signal vs next-day returns).

## Stochastic control viewpoint (hedging & execution)

Re-hedging and execution are naturally read as **path-dependent control** problems under incomplete models. I am especially interested in signatures / neural operators as representations when the state is not low-dimensional Markov—see the BNP Data & AI Lab notes in the [CV](/cv/) for the internship framing.

## How to cite / reuse

If you build on the public code, please cite the **repository URL** and **commit hash** you used. Markets evolve; pinned revisions keep empirical claims auditable.
