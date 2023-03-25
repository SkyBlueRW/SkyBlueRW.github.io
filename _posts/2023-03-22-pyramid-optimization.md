#

## Conviction Pyramid of Portfolio Construction

### dfraft

- [Introduction](#introduction)


![Image of Pyramid](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/portfolio_pyramid.png)

*Hallerbach(2015): Advances in Portfolio Risk Control*

### Introduction <a name="introduction"></a>


Ever since the birth of Mordern Portfolio Theory, mean variance optimization has taken a significant presence in portfolio construction, shifting the "science and art" blend in portfolio construction a bit more toward the science angle. However, mean variance optimization is almost "notoriously" sensitive to small estimations errors in inputs especially when estimations on return are risk are not well aligned. 

Following the dot-com and subprime crises, investors took the hard to way to realize that parameter estimations are not as reliable as once believed. In face of the questions like "what if we can not reliably forecast expected return, or correlation or even volatility?" A lot of variants of portfolio construction methods that are more risk centric such as risk weighted, risk parity, and maximum diversification are developed. 

Hallerbach(2015) introduced a nice decision pyramid of portfolio construction, which links these portfolio construction methods with increasing requirments and difficulties on estimation. The pyramid starts from a scenario where nothing can be predicted, up to a situation where both mean and variance are well understood. Ultimately, the choice of method depends on the level of confidence we have in our forecast.

In this blog post, I will try to delve into portfolio construction methods along Hallerbach's decision pyramid. The objective is to get an intuitive understanding of each method by examining their marginal conditions and aligning them with the mean variance efficient portfolio and each other.

### 



$$
\begin{aligned}
\dfrac{\partial R^{e}}{\partial w_i} / \dfrac{\partial \sigma}{\partial w_i} &= \dfrac{\partial R^{e}}{\partial w_j} / \dfrac{\partial \sigma}{\partial w_j} \\
\dfrac{\partial R^{e}}{\partial w_i} &= r^{e}_i \\
\dfrac{1}{r^{e}_i} \dfrac{\partial \sigma}{\partial w_i} &= \dfrac{1}{r^{e}_j} \dfrac{\partial \sigma}{\partial w_j} \\
\end{aligned}
$$

beyond mathematical definition with solid financial interpretation. is percentage contribution to loss

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

