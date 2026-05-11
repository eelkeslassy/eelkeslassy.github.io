---
layout: page
title: research proposal
nav: true
nav_order: 4
permalink: /research/proposal/
description: Signature-based generative Neural SDEs, path signatures, and FEDONets for LOB microstructure.
toc:
  sidebar: left
---

# Research Proposal: Signature-based Generative SDEs for Non-Markovian Microstructure Synthesis

---

## Abstract

The exponential evolution of high-frequency algorithmic trading has placed Limit Order Book (LOB) modeling at the epicenter of financial engineering and market microstructure. Historically, liquidity dynamics have been modeled through Markovian frameworks, ranging from "zero-intelligence" queues to variable-intensity Poisson processes. However, empirical evidence demonstrates that intraday liquidity is profoundly **non-Markovian**, characterized by strict path-dependency, long-memory effects, and **rough volatility** with a Hurst exponent $H < 0.5$. Current deep-learning-based synthetic data generators, such as Generative Adversarial Networks (GANs) and diffusion models, systematically fail to reproduce universal stylized facts like concave market impact or to anticipate the non-linear dynamics of flash crashes.

This research report formulates an unprecedented scientific proposal to bridge this gap: the development of **Generative Neural Stochastic Differential Equations (Neural SDEs)**, conditioned by **Path Signatures** derived from Rough Path Theory. This approach replaces inherently unstable adversarial training with divergence minimization on path space via **Signature Kernel Scores**. To address the prediction of liquidity regime shifts—specifically the abrupt transition from a liquid state to a "frozen order book"—this framework integrates operator learning via **Fourier-Embedded Deep Operator Networks (FEDONets)**.

The association of the tensor algebra of signatures to capture structural asymmetry (notably via the **Lévy Area** for cross-asset lead-lag relations) and DeepONet architectures allows for modeling microstructural phase transitions as solutions to **Stochastic Partial Differential Equations (SPDEs)**. Designed for massive deployment on ultra-high-frequency **LOBSTER** data, this methodology offers a decisive advantage. It enables a shift from terminal distribution-based risk management to **"Geometric Risk Management,"** providing direct applications for optimal execution and systemic risk compliance within institutional trading desks located in Paris, Île-de-France.

---

## 1. Introduction and Problem Definition

Modern financial microstructure is fundamentally governed by the LOB mechanism, a complex data structure operating as a continuous double auction where latent supply and demand aggregate. In this ecosystem, price formation is no longer considered an exogenous process governed by macro fundamentals, but an **endogenous emergence** resulting from the myriad infinitesimal interactions between limit orders, market orders, and cancellations. Consequently, the ability of a financial institution to simulate LOB spatio-temporal dynamics with high stochastic fidelity has become an absolute imperative for backtesting market-making algorithms and quantitative transaction impact assessment.

Early microstructure modeling paradigms relied almost exclusively on Markovian assumptions for analytical tractability. "Zero-intelligence" models, treating order arrivals and cancellations as independent Poisson processes, form the historical bedrock of this literature. While mathematically elegant, these models possess a critical flaw: they assume event independence and generate a strictly linear market impact relative to volume, contradicting empirical reality which demonstrates a pronounced concavity (the **Square Root Law**). To address this, research shifted toward Queue-Reactive models, where point process intensity depends on the instantaneous state of the book. While improving resilience modeling, these models still struggle to generate endogenously self-excited order flows.

The true epistemological break occurred with the introduction of multidimensional nearly-unstable Hawkes processes. Foundational research from the Franco-Swiss school of quantitative finance has shown that high-frequency trading (HFT) behaviors generate power-law decay kernels. The scaling limit of these microscopic Hawkes processes converges asymptotically to macroscopic stochastic processes exhibiting **rough volatility**. This roughness, characterized by a fractional Brownian motion with a singularly low Hurst exponent ($H < 0.5$, typically $\approx 0.1$), mathematically formalizes the anti-persistence and long memory inherent in microstructure. However, while these parametric models have revolutionized our understanding, they suffer from structural rigidity that limits their ability to synthesize the full high-dimensional depth of a real LOB across multiple levels.

Faced with the curse of dimensionality, the quantitative research community turned to Deep Learning. Predictive architectures like *DeepLOB* have proven the superiority of CNNs and LSTMs in extracting spatial features and anticipating micro-price movements. Simultaneously, the need for synthetic data generators has catalyzed the emergence of GANs and Probabilistic Diffusion models.

However, a rigorous analysis reveals a systemic flaw: the absence of an algebraic modeling of trajectory geometry. Financial markets undergo abrupt regime transitions, liquidity traps, and flash crashes dictated by the **topology of the path** taken by prices and volumes. These phenomena, the quintessence of path-dependency, require a formalism capable of transcending Markovian smoothing. This proposal aims to bridge this gap by articulating a framework combining Rough Path Theory, continuous Generative SDE dynamics, and Operator Learning via DeepONets.

---

## 2. Literature Review: Limits of Contemporary Simulators

A critical deconstruction of dominant methodologies highlights severe mathematical and computational limits that invalidate their use for synthesizing truly non-Markovian and reactive microstructure.

### 2.1. Generative Adversarial Networks (GANs)

The use of CGANs and WGAN-GP relies on a zero-sum game between a generator and a discriminator. Despite apparent success on short horizons, these models struggle with non-stationarity. A major issue is the endemic susceptibility to **mode collapse** and gradient instability. In microstructure, mode collapse results in truncated learning where the generator merely reproduces high-liquidity regimes, failing to generate the rare events and fat-tail distributions characteristic of market dislocations. Furthermore, GANs fail to integrate the physical laws of market impact; they often generate linear responses or erratic behavior, failing to capture the structural autocorrelation of order flow.

### 2.2. Probabilistic Diffusion Models (DDPM)

Models such as *DiffLOB* or *TRADES* reverse a diffusion SDE via score matching. While they surpass GANs in distribution fidelity, they suffer from:

1. **Markovian Smoothing:** The forward diffusion process smooths the financial trajectory, obliterating microscopic roughness ($H < 0.5$) and destroying information contained in high-frequency infinitesimal variations.
2. **Counterfactual Rigidity:** The reverse diffusion process makes interactive, reactive simulation computationally expensive and prone to stochastic error accumulation over long sequences.

| Model Type | Microstructural Limits | Mathematical/Computational Limits |
| :--- | :--- | :--- |
| **GANs** | Inability to model concave market impact; failure on fat-tail events. | Chronic gradient instability; vulnerability to **mode collapse**. |
| **Diffusion** | Markovian smoothing destroying empirical roughness ($H < 0.5$). | Prohibitive inference cost; stochastic error accumulation. |
| **Recurrent** | Discrete treatment blind to continuous inter-event dynamics. | Irreversible loss of geometric info between unequal timestamps. |

---

## 3. Fundamental Theoretical Framework: Volatility Roughness, Signatures, and Neural SDEs

### 3.1. Rough Volatility and Fractional Brownian Motion

Empirical investigation has proven that volatility is intrinsically rough ($H \in [0.05, 0.15]$). In a **Rough Bergomi** model, the instantaneous variance $V_t$ is driven by a singular kernel stochastic integral:

$$V_t = \xi_0(t) \exp \left( \eta \sqrt{2H} \int_0^t (t-s)^{H-1/2} dW_s - \frac{1}{2} \eta^2 t^{2H} \right)$$

where $W_t$ is a Brownian motion, $\eta$ is the vol-of-vol, and the kernel $(t-s)^{H-1/2}$ induces the short-term singularity responsible for roughness.

### 3.2. Rough Path Theory and Signature Algebra

To manage differential equations driven by non-semimartingale processes, Rough Path Theory studies the **Signature** of a path $X \in C([0,T], \mathbb{R}^d)$, defined as the collection of its iterated integrals in the tensor algebra $T((\mathbb{R}^d))$:

$$\mathbf{S}(X)_{0,t} = \left( 1, \int_0^t dX_{s_1}, \int_0^t \int_0^{s_2} dX_{s_1} \otimes dX_{s_2}, \dots, \int_{0 < s_1 < \dots < s_k < t} dX_{s_1} \otimes \dots \otimes dX_{s_k} \right)$$

The **Stochastic Lévy Area**, representing the anti-symmetric part of the second-order tensor, is defined as:

$$A(X^{(i)}, X^{(j)})_{0,t} = \frac{1}{2} \int_0^t (X_s^{(i)} \circ dX_s^{(j)} - X_s^{(j)} \circ dX_s^{(i)})$$

It captures asynchronous lead-lag relations invisible to linear correlation metrics.

### 3.3. Neural SDEs and Signature Kernels

We propose Neural SDEs where drift $\mu_\theta$ and diffusion $\sigma_\theta$ are parameterized by deep neural networks. The generated LOB dynamics $\hat{X}_t$ follow:

$$d\hat{X}_t = \mu_\theta(t, \hat{X}_t) dt + \sigma_\theta(t, \hat{X}_t) \circ dW_t$$

Calibration is performed by minimizing the **Maximum Mean Discrepancy (MMD)** using the **Signature Kernel** $k_{\mathrm{sig}}(X, Y) = \langle \mathbf{S}(X), \mathbf{S}(Y) \rangle_{\mathcal{H}}$:

$$\mathcal{L}(\theta) = \mathbb{E}_{P,P}[k_{\mathrm{sig}}(X, X')] - 2\mathbb{E}_{P,Q_\theta}[k_{\mathrm{sig}}(X, \hat{X})] + \mathbb{E}_{Q_\theta,Q_\theta}[k_{\mathrm{sig}}(\hat{X}, \hat{X}')]$$

This can be calculated exactly by solving a hyperbolic **Goursat PDE problem**, allowing for backpropagation with constant memory via the stochastic adjoint sensitivity method.

---

## 4. Operator Learning (DeepONets) for Liquidity Transitions

Predicting "frozen order books" requires solving **Stochastic Partial Differential Equations (SPDEs)**. We integrate **Fourier-Embedded Deep Operator Networks (FEDONets)** to approximate the non-linear operator $G$:

$$G_\theta(u)(y) = \sum_{k=1}^p b_k(u) \cdot t_k(y)$$

The **Branch Network** $b_k(u)$ ingests historical signature evaluations, while the **Trunk Network** $t_k(y)$ captures high-frequency gradients characteristic of liquidity shocks via random Fourier feature embeddings.

---

## 5. Scientific Novelty Statement

1. **Geometry vs. Distribution:** We model the **temporal topology** of microstructure rather than marginal distributions, linearizing once-intractable path-dependencies.
2. **Stability:** Elimination of adversarial training via the Signature Kernel ensures a strictly proper score and unique global minimum.
3. **Phase Transition Prediction:** FEDONet offers the first "mesh-free" early warning signal for liquidity evaporation.

---

## 6. Methodology and Implementation

1. **Projection:** Condense raw **LOBSTER** data into invariants: micro-price, spread, and Order Flow Imbalance (OFI).
2. **Signatures:** Extract log-signatures using `signatory` to capture lead-lag geometry.
3. **Generation:** Implement Neural SDEs with `torchsde`, utilizing adjoint sensitivity for $O(1)$ memory.
4. **Optimization:** Use the Signature Kernel Score calculated via GPU-accelerated Goursat solvers.
5. **Validation:** Use the **LOB-Bench** framework to verify concave market impact and transaction volume power-law autocorrelation.

---

## 7. Strategic Impact

### 7.1. Systematic Alpha

Trading algorithms can be trained against a "Digital Twin" of Euronext. The FEDONet signals the agent to stop liquidation before the book "freezes," saving basis points in slippage.

### 7.2. Geometric Risk Management

Under **FRTB (Basel IV)**, banks must isolate Non-Modellable Risk Factors. We propose **Signature Expected Shortfall (S-ES)**. By quantifying lead-lag decay and path topology, residual risks are transformed into modellable "Geometric Greeks," enabling capital requirement compression.

---

## Conclusion

The convergence of Rough Path Theory, Neural SDEs, and FEDONets provides a rigorous mathematical path to master high-frequency market toxicity. This proposal moves beyond blind distribution matching toward a deterministic understanding of path-dependency, ensuring both systemic alpha and systemic stability.

---

<p class="muted"><a href="/research/">← Back to research overview</a></p>
