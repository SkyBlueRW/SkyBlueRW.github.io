#

## Risk discipline for Drawdown Control

- [Introduction](#introduction)
- [Optimal Holding in Risky Asset](#optimal)
- [More](#more)
- [Reference](#ref)

### Introduction <a name="introduction"></a>

As discussed in a previous blog [From Volatility to Maximum Drawdown](https://skybluerw.github.io/2023/10/15/max-drawdown.html), maximum drawdown, though attracts significant attention for the evaluation of investments, is not obvious to analyze or control in practice. Following on the previous discussion on factors impacting the maximum drawdown, we will explore some viable ways to incorporate controls on drawdown risk explicitly in the portfolio management process. 

It's hard to disagree that the judgement of market condition at critical point is usually what matters for the control of maximum drawdown. In a lot of times, reasonable judgement about if the strategy is still working coupled with rule of thumbs of portfolio adjustment like risk off in case of x amount of realized loss can protect a portfolio reasonably from drawdown. While the explict incorporation of drawdown control into portfolio construction process would add additional value, especially from the perspective of a systematic portfolio construction process. It would be befiniticial for ex-post attribution, it would also help to translate any judgements into languages of portfolios or even to fill in the place in the absence of strong judgement.

In this blog, we'd like to look into some useful tools with the aim. Specifically, we will look into the discipline on risky asset holding that Grossman & Zhou (1993) initially proposed. In the case of one riskless asset and one risky asset, a fixed proportion of the difference between current wealth and acceptable maximum drawdown can be invested on risky asset to achieve largest expected utility growth while fulffilling the maximum drawdown threshold. 

The optinal proportion is jointly determined by expected return, volatility of the risky asset and risk aversion. It can be used as a reference in a two step portfolio construction process: determine the risky asset mix first and then set the leverage on the risk asset mix with reference to the discipline. It can aslo bear additional flexibility with expansion to the scenario of multi asset class hence supporting more delibrated management of strategies and asset classes.


### Optimal Holding in Risky Asset <a name="optimal"></a>

To account for maximum drawdown explicitly, Grossman & Zhou (1993) added a hard constraint on maximum drawdown ($$W_t \geq \alpha M_t$$) upon the classical portfolio optimization problem of maximizing the long term expected utility growth ($$lim_{T\to \infty} \dfrac{1}{(1-A)T}lnE[(1-A)U(W_T)]$$) with power utility ($$U(W) = \dfrac{W^{1-A}}{1-A}$$).

The risky asset is assumed to follow a Geometric Brownian motion ($$dP_t = P_t((\mu + r) dt + \sigma dZ_t)$$). With $$X_t$$ amount of wealth ($$W_t$$) invested in risky asset and the remaining in riskless asset, we have the wealth following the following stochastic process:

$$
\begin{aligned}
dW_t &= X_t ((\mu + r) dt + \sigma dZ_t) + (W_t - X_t) r dt \\
     &= r W_t dt + X_t (\mu dt + \sigma dZ_t) \\
\end{aligned}
$$

The drawdown is defined to account for the time value since the the time of peak($$W^{\pi}_t &= Max_{0\leq s\leq t}(W^{\pi}_s e^{-r(t-s)}) $$)


### More <a name="more"></a>


$$
\begin{aligned}
U(W) &= \dfrac{W^{1-A}}{1-A} \\ 
W^{\pi}_t &= Max_{0\leq s\leq t}(W^{\pi}_s e^{-r(t-s)}) \\
& lim_{T\to \infty} \dfrac{1}{(1-A)T}lnE[(1-A)U(W_T)] \\
& lim_{T\to \infty} \dfrac{1}{T}lnE[W^{1-A}_T] \\
W_t &\geq \alpha M_t \\
\end{aligned}
$$

$$
\begin{aligned}
dP_t &= P_t((\mu + r) dt + \sigma dZ_t) \\
dW_t &= X_t ((\mu + r) dt + \sigma dZ_t) + (W_t - X_t) r dt \\
     &= r W_t dt + X_t (\mu dt + \sigma dZ_t) \\
X_t &= \dfrac{\mu}{\sigma^2} \dfrac{1}{(1 - \alpha)A + \alpha} (W_t - \alpha M_t)
\end{aligned}
$$




![Gaussian](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/mdd_call_delta.png)

source: [Vecer (2006): Maximum Drawdown and Directional Trading](http://www.stat.columbia.edu/~vecer/maxdrawdown3.pdf)

### Reference <a name="ref"></a>
- Grossman & Zhou (1993): Optimal Investment Strategies For Controlling Drawdowns
- Cvitanic & Karatzas (1994): On Portfolio Optimization Under "Drawdown" Constraints
- Vecer (2006): Maximum Drawdown and Directional Trading
- Busseti, Ryu & Boyd (2016): Risk-Constrained Kelly Gambling

