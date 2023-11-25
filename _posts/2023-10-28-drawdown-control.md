#

## Risk discipline for Drawdown Control

- [Introduction](#introduction)
- [Optimal Holding in Risky Asset](#optimal)
- [More](#more)
- [Reference](#ref)

### Introduction <a name="introduction"></a>

As discussed in a previous blog [From Volatility to Maximum Drawdown](https://skybluerw.github.io/2023/10/15/max-drawdown.html), maximum drawdown, though attracts significant attention at evaluation of investments, is not obvious to analyze or control in practice. Following on the previous discussion on the factors impacting the maximum drawdown, we will explore some viable ways to incorporate explicit control on drawdown risk in the portfolio construction process. 

It is true that the judgement on market condition and strategy efficacy at critical point is what matters the most for the control of maximum drawdown. While handy and explicit tools that can help to translate these judgements into languages of portfolios or even to fill in the place in the absence of strong judgement are also critical. In this blog, we'd like to look into some useful tools with the aim. 

Specifically, we will look into the discipline on risky asset holding that Grossman & Zhou (1993) initially proposed. In the case of one riskless asset and one risky asset, a fixed proportion of the difference between current wealth and acceptable maximum drawdown can be spent on risky asset to achieve largest expected utility growth while fulffilling the maximum drawdown threshold. 

The optinal proportion is jointly determined by expected return, volatility of the risky asset and risk aversion. It can be used as a reference in a two step portfolio construction process: determine the risky asset mix first and then set the leverage on the risk asset mix with reference to the discipline. It can aslo bear additional flexibility with expansion to the scenario of multi asset class hence supporting more delibrated management of strategies and asset classes.


### Optimal Holding in Risky Asset <a name="optimal"></a>

Grossman & Zhou (1993) sets a quite classical portfolio optimization problem: maximizing the long term expected utility growth ($$lim_{T\to \infty} \dfrac{1}{(1-A)T}lnE[(1-A)U(W_T)]$$) with hard constraint on maximum drawdown (W_t \geq \alpha M_t ) and power utility ($$U(W) &= \dfrac{W^{1-A}}{1-A}$$).

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

