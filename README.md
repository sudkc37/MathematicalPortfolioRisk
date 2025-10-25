                                  Portfolio Optimization and Risk Assessment: A Mathematical Framework for Value-at-Risk Assessment and Stochastic Price Simulation


This presents a comprehensive computational framework for portfolio optimization and risk assessment, integrating classical mean-variance optimization with stochastic simulation methods. We implement three distinct portfolio construction strategies: Minimum Variance Portfolio (MVP), Tendency Portfolio, and Desired Portfolio, utilizing variance-covariance matrix estimation from historical equity data. Risk quantification is performed through parametric Value at Risk (VaR) calculations at multiple confidence levels. Furthermore, we employ Geometric Brownian Motion (GBM) to simulate forward-looking price trajectories over a three-month horizon, providing probabilistic forecasts of portfolio performance. The methodology demonstrates the practical application of optimization theory, numerical linear algebra, and stochastic calculus to quantitative finance, offering a robust framework for portfolio management decision-making under uncertainty.

 ## 1. Methodology ##
 
This research extends classical optimization by incorporating advanced risk metrics and stochastic simulation. I analyze nine securities (TSLA, AAPL, NVDA, TSM, ABEV, VTEB, V, AMD, BA) using seven years of daily prices, employing covariance matrix estimation, analytical portfolio optimization, Monte Carlo simulation for risk assessment, and path-dependent stochastic modeling.

 ## 2. Mathematical Foundation ##
 
 2.1 Covariance Matrix Estimation

The covariance matrix **Σ ∈ ℝⁿˣⁿ** captures the variance–covariance structure of asset returns.  
For assets *i* and *j*:

$$ \text{Cov}(X, Y) = \frac{1}{n} \sum_{i=1}^{n} (X_i - \bar{X})(Y_i - \bar{Y}) $$

- **Diagonal elements** (σᵢᵢ) represent individual asset variances.  
- **Off-diagonal elements** (σᵢⱼ) measure co-movement between assets *i* and *j*.

We use **logarithmic returns**:

rₜ = ln(Pₜ / Pₜ₋₁)

Log returns are preferred for their **additive property** and **approximate normality**, and are **annualized** using 252 trading days.


## Minimum Variance Portfolio and Tendency Portfolio Efficient Frontier:
<img width="727" alt="Screenshot 2024-11-05 at 11 00 58 AM" src="https://github.com/user-attachments/assets/1364554e-dddf-4e49-9b07-5cb91bebab03">

## Minimum Variance Portfolio Var:

<img width="783" alt="Screenshot 2024-11-05 at 11 04 42 AM" src="https://github.com/user-attachments/assets/69de274c-9a46-478e-948a-6194fcc05ec7">

## Tendency Portfolio Var:
<img width="793" alt="Screenshot 2024-11-05 at 11 06 04 AM" src="https://github.com/user-attachments/assets/fe2425d8-bbbd-49f7-91ed-8a8e89215610">

## Desired Portfolio Var:
<img width="793" alt="Screenshot 2024-11-05 at 11 06 49 AM" src="https://github.com/user-attachments/assets/039abd2e-5f0c-47bf-bf3b-159878b96428">

## Efficient Frontier for MVP Vs Tendency Vs Desired Portfolio:
<img width="793" alt="Screenshot 2024-11-05 at 11 07 55 AM" src="https://github.com/user-attachments/assets/f3f55755-32f0-4681-92ce-d7cc20f0181f">

<img width="936" alt="Screenshot 2024-11-05 at 11 13 55 AM" src="https://github.com/user-attachments/assets/5e3b5a94-a85f-4744-a6f6-f7d1f4a7b8e4">


## Simulated Value of Minimum Variance Portfolio:
<img width="770" alt="Screenshot 2024-11-05 at 11 09 03 AM" src="https://github.com/user-attachments/assets/6c5ab1fa-a78a-4c39-b783-40ee39969a2c">

## Simulated Value of Tendency Portfolio:
<img width="758" alt="Screenshot 2024-11-05 at 11 09 46 AM" src="https://github.com/user-attachments/assets/4bbd28e1-d0a0-4219-9e70-734664491148">

## Simulated Value of Desired Portfolio:
<img width="758" alt="Screenshot 2024-11-05 at 11 10 21 AM" src="https://github.com/user-attachments/assets/0019d66e-1653-4a24-9b7a-4e12e134f3c5">

## Simulated Price of Individual Assets:
<img width="893" alt="Screenshot 2024-11-05 at 11 12 18 AM" src="https://github.com/user-attachments/assets/28d120e5-80c1-498d-a4cb-2ec9d0fd5d1f">

<img width="893" alt="Screenshot 2024-11-05 at 11 12 34 AM" src="https://github.com/user-attachments/assets/ad4fd576-dbf5-43cb-b430-c6e77d6ae0fb">



