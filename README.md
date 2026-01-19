# Quant GANs — Research Replication

### Overview
This project presents a replication study of the paper
[“Quant GANs: Deep Generation of Financial Time Series” (Wiese et al., 2020)](https://arxiv.org/abs/1907.06673).

The objective of the original work is to propose a deep learning framework for synthetic financial time series generation, a central problem in quantitative finance with applications in risk management, derivative pricing, portfolio construction, and strategy backtesting.

Unlike traditional Monte Carlo simulations, the proposed approach relies on Generative Adversarial Networks (GANs) combined with Temporal Convolutional Networks (TCNs) to model long-term temporal dependencies and reproduce key stylized facts of financial returns.

### Methodology
The Quant GANs framework consists of:
* A TCN-based Generator producing synthetic log-returns
* A TCN-based Discriminator distinguishing real from generated data

This architecture allows the model to capture:
* Distributional properties (mean, variance, skewness, kurtosis)
* Autocorrelation structure
* Volatility clustering
* Leverage effect
Due to limited implementation details in the original paper, architectural and training choices were derived from related literature on GANs and TCNs.

### Implementation Notes
Several challenges were encountered during replication:
* Lambert-W transformation was reimplemented in Python based on the original R package and Georg’s methodology.
* The C-SVNN model was not implemented; a pure TCN risk-neutral formulation was adopted instead.
* Two preprocessing pipelines were compared: with and without Lambert-W transformation.

While the Lambert-W approach improved normality, it introduced instability and extreme outliers after inverse transformation. The non-transformed pipeline produced faster convergence and more stable results.

### Evaluation
Model performance is assessed using financial and statistical metrics:
* First four moments (mean, variance, skewness, kurtosis)
* DY metric
* ACF score
* Leverage effect score

These metrics are also used to control training convergence.
