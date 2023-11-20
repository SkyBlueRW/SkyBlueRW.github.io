#

## Risk discipline for Drawdown Control

- [Introduction](#introduction)
- [Optimal Holding in Risky Asset](#optimal)
- [More](#more)
- [Reference](#ref)

As discussed in a previous blog [From Volatility to Maximum Drawdown](https://skybluerw.github.io/2023/10/15/max-drawdown.html), maximum drawdown, though attracts significant attention when evaluating an investment, is not obvious to analyze or control in practice.  

continuously reallocating wealth between a risk asset distributed with Geometric Brownian Motion and a riskless asset.

For stochastic optimal control problems, the auxiliary optimal control problem is a convex relaxation of the original problem. In the case of stochastic minimization problems, the relaxation gives provable lower bounds on the true optimal value

### Introduction <a name="introduction"></a>


### Optimal Holding in Risky Asset <a name="optimal"></a>


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

### Reference <a name="ref"></a>
- Grossman & Zhou (1993): Optimal Investment Strategies For Controlling Drawdowns
- Cvitanic & Karatzas (1994): On Portfolio Optimization Under "Drawdown" Constraints
- Vecer (2006): Maximum Drawdown and Directional Trading
- Busseti, Ryu & Boyd (2016): Risk-Constrained Kelly Gambling

