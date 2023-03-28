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

The marginal contribution to excess return of a constituent is simply its excess return. Thus we have

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

In theory, the Maximum Sharpe ratio Portfolio (MSRP) is the optimal portfolio for all investors, as it allows them to maximize expected returns for each unit of risk taken. Investors can adjust their leveage on MSRP to acheice a desired risk profile. However, accurate estimation of expected returns and the covariance matrix is crucial for achieving these results, and such estimations are not always readily available. When estimation errors occur, they can have a significant impact on the MSRP. 

Without additional constraints, MSRP will consider our inputs as truth without any uncertainty and attempt to arbitrage with small differences within them, often unrealistically. For instance, if we estimate two securities with expected return of 10.5% and 10.7%, respectively, we do not want to place a heavy bet based on such a small difference. However, MSRP may view this as a serious arbitrage opportunity, especially if the two securities have a high correlation. Such kind of unreasonable bets can result in a highly concentrated and unrealistic portfolio, which performs badly out of sample.


### Risk centric Portfolio Construction <a name="risk"></a>

Risk-centric portfolio construction methods can help address scenarios where reliable estimation is not available for certain inputs. While these methods represent a compromise in the absence of reliable estimation, portfolios generated using these methods can be robust and perform comparably well to the MSRP in certain market scenarios, as suggested by their marginal conditions. These portfolios are not dependent on full knowledge of return and risk, providing a conservative alternative with a solid bottom line and some upside potential for investors.

**Equal Weighted Portfolio (EWP)**

**Risk Weighted Portfolio (RWP)**

**Minimum Variance Portfolio (MVP)**

$$
\begin{aligned}
\dfrac{\partial \sigma}{\partial w_i} &= \dfrac{\partial \sigma}{\partial w_j}
\end{aligned}
$$

**Risk Parity Portfolio (RPP)**

$$
\begin{aligned}
w_i \dfrac{\partial \sigma}{\partial w_i} &= w_j \dfrac{\partial \sigma}{\partial w_j}
\end{aligned}
$$


**Maximum Diversification Portfolio (MDP)**


$$
\begin{aligned}
\dfrac{1}{\sigma_i} \dfrac{\partial \sigma}{\partial w_i} &= \dfrac{1}{\sigma_j} \dfrac{\partial \sigma}{\partial w_j}
\end{aligned}
$$


### Reference
- Hallerbach (2015): Advances in Portfolio Risk Control
- Qian (2006): On the Financial Interpretation of Risk Contribution: Risk Budgets do add up
- Choueifaty (2008): Torward maximum diversification
- Haesen, Hallerbach & Markwat (2017): Enhancing Risk Parity by Including Views


