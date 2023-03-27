#

## Conviction Pyramid of Portfolio Construction

### dfraft

- [Introduction](#introduction)
- [Maximum Sharpe Ratio Portfolio](#msrp)
- [Risk Centric Portfolio Construction](#risk)



![Image of Pyramid](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/portfolio_pyramid.png)

*Hallerbach(2015): Advances in Portfolio Risk Control*

### Introduction <a name="introduction"></a>


Ever since the birth of Mordern Portfolio Theory, mean variance optimization has taken a significant presence in portfolio construction, tilting the "science and art" blend a bit more toward the former. However, mean variance optimization is almost "notoriously" sensitive to small estimation errors in inputs, particularly when return and risk estimates are not well aligned.

It is especially true after the dot-com and subprime crises when investors took the hard way to realize that parameter estimations are not as reliable as once thought. In facing of questions like "what if we cannot reliably forecast expected return, correlation, or volatility?", risk-centric portfolio construction techniques that rely less on estimation, such as risk-weighted, risk parity, and maximum diversification, were created.

Hallerbach(2015) introduced a nice decision pyramid of portfolio construction, which links these portfolio construction methods with increasing input estimation requirements and difficulties. The pyramid starts from a scenario where nothing can be predicted, up to a situation where both mean and variance are well understood. 

The choice among these portfolio construction methods then depends on how confident are we in our forecasts. On one hand, the more reliable information we can feed into the portfolio construction process, the better performance we can expect from the portfolio. While on the other hand, poor estimation often have a detrimental negative impact on the portfolio. 

In this blog post, I will try to delve into portfolio construction methods along Hallerbach's decision pyramid. The objective is to gain some intuitive understanding of each method by examining their marginal conditions and aligning them with the mean variance efficient portfolio and each other.

### Maximum Sharpe Ratio Portfolio <a name="msrp"></a>

Let's begin by setting the benchmark with the Maximum Sharpe Ratio Portfolio (MSRP). It is the tangent portfolio on the efficient frontier with highest sharpe ratio ($$\dfrac{R - R^{f}}{\sigma} = \dfrac{R^{e}}{\sigma}$$) across the opportunity set. 

![Image of Tangency](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/Tangency%20portfolio.jpg)

*Source: wikipedia*

The portfolio's marginal condition offers nice insights. For a portfolio to be MSRP, the ratio of marginal contribution to excess return to marginal contribution to volatility from all constituents should align. Otherwise, one can improve the Sharpe ratio further by overweighting constituents with a higher marginal ratio.

$$
\begin{aligned}
\dfrac{\partial R^{e}}{\partial w_i} / \dfrac{\partial \sigma}{\partial w_i} &= \dfrac{\partial R^{e}}{\partial w_j} / \dfrac{\partial \sigma}{\partial w_j} \\
\end{aligned}
$$

The marginal contribution to excess return of a constituent is simply its excess return. Thus

$$
\begin{aligned}
\dfrac{\partial R^{e}}{\partial w_i} &= r^{e}_i \\
\dfrac{1}{r^{e}_i} \dfrac{\partial \sigma}{\partial w_i} &= \dfrac{1}{r^{e}_j} \dfrac{\partial \sigma}{\partial w_j} \\
\end{aligned}
$$

It's worth mentioning that marginal contribution to volatility also plays a crucial role in portfolio analytics. It leads to an addible attribution of portfolio volatility to each constituent. Qian (2006) further linked the marginal contribution to volatility to conditional percentile contribution of loss, providing a nice financial interpretation for the quantity.

$$
\begin{aligned}
\sum_i w_i \dfrac{\partial \sigma}{\partial w_i} &= \sigma
\end{aligned}
$$

Theoretically, MSRP is the only portfolio that makes sense to all investors. Investors should scale their leverages on the portfolio to achieve a desried risk profile for the most efficient risk-taking. That is getting the most expected return for every bit of risk taken. However, this requires good estimation of both expected returns and the covariance matrix, which we do not always have.

Without additional constraints, MSRP will consider our inputs as truth without any uncertainty and attempt to arbitrage with small differences in estimation, often unrealistically. For instance, if we estimate two securities with expected return of 10.5% and 10.7%, respectively, we do not want to place a heavy bet based on such a small difference due to high standard error embedded in return estimation. However, MSRP may view this as a serious arbitrage opportunity, especially if the two securities have a high correlation. Such kind of unreasonable bets can result in a highly concentrated and unrealistic portfolio, which performs badly out of sample.

### Risk centric Portfolio Construction <a name="risk"></a>


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
- Roncalli : Introduction to Risk Parity and Budgeting




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

