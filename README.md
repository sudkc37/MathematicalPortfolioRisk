                                  Portfolio Optimization and Risk Assessment: A Mathematical Framework for Value-at-Risk Assessment and Stochastic Price Simulation


This presents a comprehensive computational framework for portfolio optimization and risk assessment, integrating classical mean-variance optimization with stochastic simulation methods. We implement three distinct portfolio construction strategies: Minimum Variance Portfolio (MVP), Tendency Portfolio, and Desired Portfolio, utilizing variance-covariance matrix estimation from historical equity data. Risk quantification is performed through parametric Value at Risk (VaR) calculations at multiple confidence levels. Furthermore, we employ Geometric Brownian Motion (GBM) to simulate forward-looking price trajectories over a three-month horizon, providing probabilistic forecasts of portfolio performance. The methodology demonstrates the practical application of optimization theory, numerical linear algebra, and stochastic calculus to quantitative finance, offering a robust framework for portfolio management decision-making under uncertainty.

 ## 1. Methodology ##
 
This research extends classical optimization by incorporating advanced risk metrics and stochastic simulation. I analyze nine securities (TSLA, AAPL, NVDA, TSM, ABEV, VTEB, V, AMD, BA) using seven years of daily prices, employing covariance matrix estimation, analytical portfolio optimization, Monte Carlo simulation for risk assessment, and path-dependent stochastic modeling.

 ## 2. Mathematical Foundation ##
 
 2.1 Covariance Matrix Estimation

The covariance matrix **Σ ∈ ℝⁿˣⁿ** captures the variance–covariance structure of asset returns.  
For assets *i* and *j*:

$$ \text{Cov}(X, Y) = \frac{1}{n} \sum_{i=1}^{n} (X_i - \bar{X})(Y_i - \bar{Y}) $$

Matrix represenatation of covariance matrix with n assets:

$$
\mathbf{\Sigma} = \begin{pmatrix}
\sigma_{11} & \sigma_{12} & \cdots & \sigma_{1n} \\
\sigma_{21} & \sigma_{22} & \cdots & \sigma_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
\sigma_{n1} & \sigma_{n2} & \cdots & \sigma_{nn}
\end{pmatrix}
$$

- **Diagonal elements** (σᵢᵢ) represent individual asset variances.  
- **Off-diagonal elements** (σᵢⱼ) measure co-movement between assets *i* and *j*.

We used **logarithmic returns**:

$$ 
\( r_t = \ln\left(\frac{P_t}{P_{t-1}}\right) \)
$$

Log returns are preferred for their **additive property** and **approximate normality**, and are **annualized** using 252 trading days.


2.2 Minimum Variance Portfolio

A minimum variance portfolio is a selection of assets that aims to minimize the overall volatility or risk of the portfolio. It achieves this by carefully allocating investments across different assets based on their historical volatilities, expected returns, and correlations with each other. The goal is to construct a portfolio where the assets' movements offset each other as much as possible, reducing the portfolio's overall risk.

Investors often use minimum variance portfolios when they prioritize capital preservation and aim to minimize downside risk. These portfolios are particularly relevant in volatile markets or for risk-averse investors who prioritize stability and are willing to accept potentially lower returns in exchange for reduced risk.

$$
\text{MPV weight} = \frac{\Sigma^{-1} \mathbf{1}}{\sum_{i=1}^{n} \mathbf{1}^\top (\Sigma^{-1}\mathbf{1})}
$$

where,

$$\Sigma^{-1}$$ is the inverse of the covariance matrix.  
$$\mathbf{1}$$ is a vector of ones.

The portfolio return is the inverse of the covariance matrix:  


$$
R_{\text{MVP}} = \frac{R' \Sigma^{-1} \mathbf{1}}{\mathbf{1}' \Sigma^{-1} \mathbf{1}}
$$

and the volatility is:  

$$
\sigma_{\text{MVP}} = \sqrt{\frac{1}{\mathbf{1}' \Sigma^{-1} \mathbf{1}}}
$$

2.3 Tangency Portfolio

A tendency portfolio is a strategy that capitalizes on persistent trends or patterns in asset prices or market behaviors. It involves selecting assets based on their historical performance trends, such as momentum or mean reversion. The goal is to exploit these tendencies to achieve superior returns.

$$
\text{TPweight} = \frac{\Sigma^{-1} \mathbf{R}_i}{\sum_{i=1}^{n} \mathbf{R}_i \,(\Sigma^{-1}\mathbf{1})}
$$
where,
$$\Sigma^{-1}\, \text{is the inverse of covariance matrix.} $$
$$\mathbf{1} \,\text{ is the matrix of 1's} $$
$$\mathbf{R} \,\text{ is the return of assets} $$

The portfolio return is:

$$
R_{\text{TP}} = \frac{R' \Sigma^{-1} R}{R' \Sigma^{-1} \mathbf{1}}
$$

and its volatility is:

$$
\sigma_{\text{TP}} = \sqrt{\frac{R' \Sigma^{-1} R}{R' \Sigma^{-1} \mathbf{1}}}
$$

2.4 Efficient Frontier and Constrained Optimization

The efficient frontier represents portfolios that maximize return for a given level of risk.  

Define the following parameters:  

$$
a = \mathbf{1}' \Sigma^{-1} \mathbf{1}, \quad
b = R' \Sigma^{-1} \mathbf{1}, \quad
c = R' \Sigma^{-1} R, \quad
d = ac - b^2
$$

Then, the efficient frontier is given by:  

$$
\sigma p^2 = \frac{a\mu_p^2 - 2b\mu_p + c}{d}
$$ 

For a target return $\mu^*$, the optimal weight vector via Lagrangian optimization is:


$$
\mathbf{w} = \frac{c - b \mu^*}{d} \, \Sigma^{-1} \mathbf{1} \; + \; \frac{a \mu^* - b}{d} \, \Sigma^{-1} \mathbf{R}
$$

This separates the weights into **risk-minimizing** and **return-targeting** components.


## Minimum Variance Portfolio and Tendency Portfolio Efficient Frontier:
<img width="727" alt="Screenshot 2024-11-05 at 11 00 58 AM" src="https://github.com/user-attachments/assets/1364554e-dddf-4e49-9b07-5cb91bebab03">


3. Value-at-Risk Analysis

VaR quantifies the **maximum expected loss** over a time horizon at a given confidence level. Formally:

$$
\text{VaR}_\alpha = \inf \{ x \in \mathbb{R} : P(L \le x) > 1 - \alpha \}.
$$

We employ **historical simulation with rolling windows**, computing portfolio returns:

$$
r_{p,t} = \sum_i w_i r_{i,t},
$$

calculating 30-day rolling returns:

$$
R_{30}(t) = \sum_{k=0}^{29} r_p(t-k),
$$

and determining the \((1-\alpha)\) percentile.  

At **95% confidence**, VaR represents the loss threshold **exceeded only 5% of the time**.  

The empirical distribution is visualized using **kernel density estimation**.


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



