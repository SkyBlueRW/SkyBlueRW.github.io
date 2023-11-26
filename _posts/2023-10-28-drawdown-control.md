#

## Risk discipline for Drawdown Control

- [Introduction](#introduction)
- [Optimal Holding in Risky Asset](#optimal)
- [More](#more)
- [Reference](#ref)

### Introduction <a name="introduction"></a>


As discussed in a previous blog [From Volatility to Maximum Drawdown](https://skybluerw.github.io/2023/10/15/max-drawdown.html), maximum drawdown, though attracts significant attention for the evaluation of investments, is not obvious to analyze or control in practice. Following on the previous discussion on factors closly linked to the maximum drawdown, we will explore some viable ways to incorporate controls on drawdown risk explicitly in the portfolio management process. 

It's hard to disagree that the judgement of market condition at critical point is usually what matters for the control of maximum drawdown. In a lot of times, reasonable judgement about if the strategy is still working coupled with rule of thumbs of portfolio adjustment like risk off in case of x amount of realized loss can protect a portfolio reasonably from drawdown. While the explict incorporation of drawdown control into portfolio construction process would add additional value, especially from the perspective of a systematic portfolio construction process. It would be befiniticial for ex-post attribution, it would also help to translate any judgements into languages of portfolios or even to fill in the place in the absence of strong judgement.

In this blog, we'd like to look into some useful tools with the aim. Specifically, we will look into the discipline on risky asset holding that Grossman & Zhou (1993) initially proposed. In the case of one riskless asset and one risky asset, a fixed proportion of the difference between current wealth and acceptable maximum drawdown can be invested on risky asset to achieve largest expected utility growth while fulffilling the maximum drawdown threshold. 

The proportion is jointly determined by expected return, volatility of the risky asset and risk aversion. It can be used as a reference in a two step portfolio construction process: determine the risky asset mix first and then set the leverage on the risk asset mix with reference to the discipline. It can aslo bear additional flexibility with expansion to the scenario of multi risky asset hence supporting more delibrated management of strategies and asset classes.


### Optimal Holding in Risky Asset <a name="optimal"></a>

To account for maximum drawdown explicitly, Grossman & Zhou (1993) added a hard constraint on maximum drawdown ($$W_t \geq \alpha \mathop{Max}_{0\leq s\leq t}{W_s}$$, $$W_t$$ is the wealth at time t, $$1 - \alpha$$ is the maximum acceptable drawdown) upon the classical portfolio optimization problem of maximizing the long term expected utility growth with power utility ($$U(W) = \dfrac{W^{1-A}}{1-A}$$). With diferent time value acounted for current wealth and previous high water, we are essentially conducting the following portfolio optimization. ($$X_t$$ is the amount of money invested in the risky asset).


$$
\begin{aligned}
\mathop{Max}_{X_t} &
\mathop{lim}_{T\to \infty} \dfrac{1}{(1-A)T}lnE[(1-A)U(W_T)] \\
& P[W_t \geq \alpha e^{rt}\mathop{Max}_{0\leq s\leq t}(W^{\pi}_s e^{-rs}), 0\leq t\leq \infty] = 1 
\end{aligned}
$$

This is not an easy problem to solve. Luckily we are standing on the shoulder of the giants :) Grossman & Zhou (1993) and Cvitanic & Karatzas (1994) solved the abovementioned stochastic control problem and derived the optiomal holding.

$$
\begin{aligned}
X_t &= \dfrac{\mu}{\sigma^2} \dfrac{1}{(1 - \alpha)A + \alpha} (W_t - \alpha M_t) \\
    &= \dfrac{\mu}{\sigma^2} \dfrac{1}{(1 - \alpha)A + \alpha} (1 - \alpha\dfrac{M_t}{W_t})W_t \\
M_t & = e^{rt}\mathop{Max}_{0\leq s\leq t}(W^{\pi}_s e^{-rs})
\end{aligned}
$$

Despite the lenghty deviation, the the result is quite intuitive of the Constant Proportion Portfolio Insurance(CPPI) type. With a constant proportion $$\dfrac{\mu}{\sigma^2} \dfrac{1}{(1 - \alpha)A + \alpha}$$ of the difference between current wealth and lowest acceptable wealth level defined by prior peak $$W_t - \alpha M_t$$ invested in risky asset, we can maximize expected power utility while restricting maximum drawdown below ($$1 - \alpha$$) almost surely. 

Larger 'safe cushion' ($$W_t - \alpha M_t$$) above the floor, better expected performance of the risky asset ($$\dfrac{\mu}{\sigma^2}$$), lower risk aversion (A) and higher acceptable maximum drawdown ($$1 - \alpha$$) lead to higher amounts of wealth allocated to the risky asset. When $$\alpha$$ is 0, the maximum drawdown constraint placed is equivalent to the bankruptcy constraint ($$W_t \geq 0$$). 

Obviously reducing the acceptable maximum drawdown ($$1 - \alpha$$) is at the cost of lower rate of wealth accumulation. Rasing the value of $$\alpha$$ from 0 to $$\alpha_1$$ scalses the long term rate of expected utility growth down by a factor of $$1 - [1 + (\dfrac{1}{\alpha_0} -1)A] ^ {-1}$$. The loss in growth rate is smaller for investors that are more risk averse or when the degree of protection on drawdown is small. 




### Putting it in application <a name="more"></a>

translation to concept that investors likely have judgement. 

Placing constraint on maximum drawdown is essentially setting a stochastic floor on the wealth defined by previous peak. It is also worth to mention that a similar optimal holding can also be derived for the case of static floor, in which case the wealth is not allowed to go below an absolute amount (K). The optimal holding then becomes

$$
\begin{aligned}
X_t &= \dfrac{\mu}{\sigma^2} \dfrac{1}{(A} (W_t - K) \\
\end{aligned}
$$

**Another Contigent Claim!**

Assuming that the risk asset follows a Geometric Brownian motion ($$dP_t = P_t((\mu + r) dt + \sigma dZ_t)$$), with $$X_t$$ amount of wealth ($$W_t$$) invested in risky asset and the remaining in riskless asset, we have the wealth following the stochastic process:

**Not Almost Sure**

$$
\begin{aligned}
dW_t &= X_t ((\mu + r) dt + \sigma dZ_t) + (W_t - X_t) r dt \\
     &= r W_t dt + X_t (\mu dt + \sigma dZ_t) \\
\end{aligned}
$$


$$
\begin{aligned}
U(W) &= \dfrac{W^{1-A}}{1-A} \\ 
W^{\pi}_t &= Max_{0\leq s\leq t}(W^{\pi}_s e^{r(t-s)}) \\
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

