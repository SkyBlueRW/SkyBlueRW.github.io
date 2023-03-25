#

## Conviction Pyramid of Portfolio Construction

### dfraft

- [Introduction](#introduction)

### Introduction <a name="introduction"></a>

![Image of Pyramid]([asset/portfolio_pyramid.png](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/portfolio_pyramid.png))

*Hallerbach(2015): Advances in Portfolio Risk Control*


Ever since the birth of Mordern Portfolio Theory, mean variance optimization is taking a significant presence in portfolio construction, making the mix of "science and art" in portfolio construction a bit toward science. While, mean variance optimization is almost "notoriously" sensitive to small estimations errors in expected return and covariance matrix. 

Especially after tech bubble and financial crisis, investors take the hard way to learn that estimation of parameters are not that easy. In face of the questions "what if we can not reliably forecast expected return, or correlation or even volatility?" A lot of variants of portfolio optimization methods that are more risk centric such as risk weighted, risk parity, and maximum diversification are developed. 

Hallerbach(2015) introduced the decision pyramid of portfolio construction, which demonstrate the increasing requirments on estimation from when you can't predict anything up to you are full aware of mean and variance. The choice then remains how confident are we in the forecast.

along the line discuss about intuition of each method via the marginal condition and compare with the benchmark of Mean Variance Optimization.


estimation error.

MSRP

$$
\begin{aligned}
\dfrac{1}{r^{e}_i} \dfrac{\partial \sigma}{\partial w_i} &= \dfrac{1}{r^{e}_j} \dfrac{\partial \sigma}{\partial w_j}
\end{aligned}
$$

$$
\begin{aligned}
\dfrac{\partial \sigma}{\partial w_i} &= \beta_{i} \sigma \\
\sum_i w_i \dfrac{\partial \sigma}{\partial w_i} &= \sigma
\end{aligned}
$$


MV

$$
\begin{aligned}
\dfrac{\partial \sigma}{\partial w_i} &= \dfrac{\partial \sigma}{\partial w_j}
\end{aligned}
$$


ERCP

$$
\begin{aligned}
w_i \dfrac{\partial \sigma}{\partial w_i} &= w_j \dfrac{\partial \sigma}{\partial w_j}
\end{aligned}
$$



MDP

$$
\begin{aligned}
\dfrac{1}{\sigma_i} \dfrac{\partial \sigma}{\partial w_i} &= \dfrac{1}{\sigma_j} \dfrac{\partial \sigma}{\partial w_j}
\end{aligned}
$$

### Reference
- Hallerbach (2015): Advances in Portfolio Risk Control
- Qian (2006): On the Financial Interpretation of Risk Contribution: Risk Budgets do add up
- Choueifaty (2008): Torward maximum diversification
- Kolm, Tutuncu & Fabozzi (2013): 60 Years of Portfolio Optimization: Practical Challenges and Current Trends




conviction in forecasting future

Marginal condition, equivalence

Despite good of Mean Variance Optimization, reliable forecast. as a starting point.

Based on forecasting
Key line: how confident: expected return, correlation, variance. How confident in forecasting.
Another line structure based on financial theory



even estimate with overlapping

1/n not easy to beat

market cap. 
CAPM unharmful -> capacity, recalibility. No clear dominant way 
idiosyncratic risk turn systematical


meaning of risk contribution

