USD/INR Volatility Forecasting using HAR-RV-X
Project Overview

This project implements a linear econometric framework to forecast the realized volatility of the USD/INR exchange rate. Instead of predicting price direction, the focus is on modeling volatility, which is more persistent, interpretable, and relevant for real-world financial applications such as hedging, risk management, and derivatives pricing.

The project progresses from a basic linear regression baseline to a Heterogeneous Autoregressive Realized Volatility model with exogenous variables (HAR-RV-X), while strictly maintaining model transparency and interpretability.

Motivation

FX returns are notoriously difficult to predict.

FX volatility exhibits clustering, persistence, and long-memory behavior.

USD/INR is a macro-sensitive and partially managed currency pair, making volatility analysis more meaningful than price forecasting.

This project demonstrates that well-structured linear models can meaningfully explain FX volatility without relying on black-box or non-linear techniques.

Key Objectives

Forecast USD/INR realized volatility using linear models

Understand why naïve linear regression fails

Implement HAR-RV-X to capture multi-horizon volatility dynamics

Maintain interpretability and economic intuition

Benchmark results against academic literature

Methodology Summary
1. Volatility Measurement

Volatility is measured using the Parkinson (1980) High–Low estimator:

𝑅
𝑉
𝑡
=
1
4
ln
⁡
(
2
)
(
ln
⁡
(
𝐻
𝑡
𝐿
𝑡
)
)
2
RV
t
	​

=
4ln(2)
1
	​

(ln(
L
t
	​

H
t
	​

	​

))
2

This estimator is more efficient than close-to-close variance and well-suited for FX markets.

2. Baseline Model

A simple OLS linear regression is used as a benchmark:

log
⁡
(
𝑅
𝑉
𝑡
)
=
𝛼
+
𝛽
log
⁡
(
𝑅
𝑉
𝑡
−
1
)
+
𝜀
𝑡
log(RV
t
	​

)=α+βlog(RV
t−1
	​

)+ε
t
	​


This model performs poorly due to volatility’s multi-horizon nature.

3. HAR-RV-X Model

The final model decomposes volatility across multiple time horizons and includes macro-financial spillovers:

log
⁡
(
𝑅
𝑉
𝑡
)
=
𝛽
0
+
𝛽
𝑑
log
⁡
(
𝑅
𝑉
𝑡
−
1
)
+
𝛽
𝑤
log
⁡
(
𝑅
𝑉
‾
𝑡
−
5
:
𝑡
−
1
)
+
𝛽
𝑚
log
⁡
(
𝑅
𝑉
‾
𝑡
−
22
:
𝑡
−
1
)
+
∑
𝛾
𝑖
𝑋
𝑖
+
𝜀
𝑡
log(RV
t
	​

)=β
0
	​

+β
d
	​

log(RV
t−1
	​

)+β
w
	​

log(
RV
t−5:t−1
	​

)+β
m
	​

log(
RV
t−22:t−1
	​

)+∑γ
i
	​

X
i
	​

+ε
t
	​


Where exogenous variables include:

DXY (USD strength)

VIX (global risk sentiment)

Brent Crude (commodity exposure)

S&P 500 and NIFTY 50 (equity spillovers)

Results

Final R² ≈ 0.44

Significant improvement over the baseline linear model

Coefficients are economically intuitive and statistically meaningful

This performance exceeds typical FX volatility benchmarks reported in literature (≈0.15–0.30).

Technology Stack

Language: Python

Data Source: yFinance

Libraries:

pandas, numpy (data handling)

statsmodels (OLS regression)

matplotlib, seaborn (visualization)

Environment: Jupyter Notebook

Project Structure
├── basic_ols_volatility.ipynb      # Baseline linear regression model
├── VITTAM_HAR_RV_X_FINAL.ipynb     # Final HAR-RV-X implementation
├── README.md                      # Project documentation

Applications

FX options pricing

Currency hedging strategies

Treasury risk management

Stress testing and scenario analysis

Limitations

Linear model only (no GARCH or ML)

Daily frequency data

Does not explicitly model regime shifts or policy interventions

These limitations are intentional to preserve interpretability.

Future Improvements

Regime-switching HAR models

HAR + GARCH hybrid frameworks

Higher-frequency (intraday) realized volatility

Inclusion of policy and interest rate variables

Key References

Corsi, F. (2009). A Simple Approximate Long-Memory Model of Realized Volatility.

Parkinson, M. (1980). The Extreme Value Method for Estimating the Variance of the Rate of Return.

Andersen, T. G., Bollerslev, T., Diebold, F. X. (2007). Roughing It Up.

Degiannakis, S., Floros, C. (2015). Volatility Spillovers Between FX and Equity Markets.

Conclusion

This project demonstrates that model structure is more important than model complexity. By combining realized volatility estimation with heterogeneous autoregressive dynamics and macro-financial spillovers, a purely linear framework can achieve strong explanatory power for FX volatility.