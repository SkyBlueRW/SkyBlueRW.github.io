#

## Risk discipline for Drawdown Control

- [Introduction](#introduction)
- [Optimal Holding for Drawdown Control](#optimal)
- [The Practical Side](#practice)
- [Reference](#ref)

### Introduction <a name="introduction"></a>


As discussed in a previous blog [From Volatility to Maximum Drawdown](https://skybluerw.github.io/2023/10/15/max-drawdown.html), maximum drawdown, though attracts significant attention for the evaluation of investments, is not obvious to analyze or control in practice. Following on the previous discussion on factors closly linked to the maximum drawdown, we will explore some viable ways to incorporate controls on drawdown risk explicitly in the portfolio management process. 

It's hard to disagree that the judgement of market condition at critical point is usually what matters for the control of drawdown risk. In a lot of times, reasonable judgement about if the strategy is still working coupled with rule of thumbs of portfolio adjustment like risk off in case of x amount of realized loss can protect a portfolio reasonably from drawdown. While the explict incorporation of drawdown control into portfolio construction process would add additional value, especially from the perspective of a systematic portfolio construction process. It would be befiniticial for ex-post attribution, it would also help to keep a consistent languages of portfolios or even to fill in the place in the absence of strong judgement.

In this blog, we'd like to look into the discipline on risky asset holding that Grossman & Zhou (1993) initially proposed with the aim. In the case of one riskless asset and one risky asset, a constant proportion of the largest acceptable loss can be invested on risky asset to achieve largest expected utility growth while fulffilling drawdown threshold. 

The discipline generally does not place additional burden of estimation. Traditional inputs to the Markowitz optimization like expected return and risk of the risky asset along with risk aversion are required for the calculation of the constant proportion. Such a optimal holding in risky asset can be used as a reference in a two step portfolio construction process: determine the risky asset mix first and then set the leverage on the risky asset mix with reference to the discipline. It can aslo bear additional flexibility with expansion to the scenarios of multi risky assets hence supporting more delibrated management of strategies and asset classes.


### Optimal Holding for Drawdown Control <a name="optimal"></a>

Assuming the existence of one risk free asset ($$rdt$$) and one risky asset ($$dP_t = P_t((\mu + r) dt + \sigma dZ_t)$$), with $$X_t$$ amount of wealth ($$W_t$$) invested in risky asset and the remaining in riskless asset, we have the wealth following the stochastic process:

$$
\begin{aligned}
dW_t &= X_t ((\mu + r) dt + \sigma dZ_t) + (W_t - X_t) r dt \\
     &= r W_t dt + X_t (\mu dt + \sigma dZ_t) \\
\end{aligned}
$$

To incorporate drawdown control explicitly, Grossman & Zhou (1993) added a hard constraint on maximum drawdown in the form of a stochastic floor determined by previous peak value ($$W_t \geq \alpha \mathop{Max}_{0\leq s\leq t}{W_s}$$, $$1 - \alpha$$ is the maximum acceptable drawdown) upon the classical portfolio optimization problem of maximizing the long term expected utility growth with power utility ($$U(W) = \dfrac{W^{1-A}}{1-A}$$). With diferent time value accounted for current wealth and previous peak value, we are essentially conducting the following portfolio optimization. ($$X_t$$ is the amount of money invested in the risky asset).


$$
\begin{aligned}
\mathop{Max}_{X_t} &
\mathop{lim}_{T\to \infty} \dfrac{1}{(1-A)T}lnE[(1-A)U(W_T)] \\
& P[W_t \geq \alpha e^{rt}\mathop{Max}_{0\leq s\leq t}(W^{\pi}_s e^{-rs}), 0\leq t\leq \infty] = 1 
\end{aligned}
$$

The above stochastic control problem is definitely not easy to solve. Luckily we are standing on the shoulder of the giants :) Grossman & Zhou (1993) and Cvitanic & Karatzas (1994) solved the problem and derived the optiomal holding analytically.

$$
\begin{aligned}
X_t &= \dfrac{\mu}{\sigma^2} \dfrac{1}{(1 - \alpha)A + \alpha} (W_t - \alpha M_t) \\
    &= \dfrac{\mu}{\sigma^2} \dfrac{1}{(1 - \alpha)A + \alpha} (1 - \alpha\dfrac{M_t}{W_t})W_t \\
M_t & = e^{rt}\mathop{Max}_{0\leq s\leq t}(W^{\pi}_s e^{-rs})
\end{aligned}
$$

Despite the lenghty derivation, the optimal holding is quite intuitive of the Constant Proportion Portfolio Insurance(CPPI) type. With a constant proportion $$\dfrac{\mu}{\sigma^2} \dfrac{1}{(1 - \alpha)A + \alpha}$$ of the difference between current wealth and lowest acceptable wealth level defined by prior peak $$W_t - \alpha M_t$$ invested in risky asset, we can maximize expected power utility while restricting maximum drawdown below ($$1 - \alpha$$) almost surely. 

Larger 'safe cushion' above the floor ($$W_t - \alpha M_t$$), better expected performance of the risky asset ($$\dfrac{\mu}{\sigma^2}$$), lower risk aversion (A) and higher acceptable maximum drawdown ($$1 - \alpha$$) safeguard higher allocation to the risky asset. 

It is also worth to mention that similar to applying the constraint on maximum drawdown, which is essentially placing a stochastic floor on the wealth, we can also place a constant amount (K) as the lowest acceptable wealth, which is a constant floor. The optimal holding is still in the form of CPPI like. Essentially replacing the stochastic floor $$\alpha M_t$$ with a constant floor $$K$$ is equivalent to adjust the risk aversion from $$(1 - \alpha)A + \alpha$$ to $$A$$.

$$
\begin{aligned}
Y_t &= \dfrac{\mu}{\sigma^2} \dfrac{1}{A} (W_t - K) \\
\end{aligned}
$$
 
The two optimal solutions of stochastic and constant floor meet at $$\alpha = 0$$. The constratint becomes a bankruptcy protection $$W_t \geq 0$$, which is likely the lowest bottom line for a lot of investors :). Obviously reducing the maximum drawdown ($$1 - \alpha$$) threshold is at the cost of lower rate of wealth accumulation. Rasing the value of $$\alpha$$ from 0 to $$\alpha_1$$ scalses the long term rate of expected utility growth down by a factor of $$1 - [1 + (\dfrac{1}{\alpha_0} -1)A] ^ {-1}$$. The loss in growth rate is smaller for investors that are more risk averse or when the degree of protection on drawdown is small. 


### The practical Side <a name="practice"></a>

Here we are with a clearly defined optimal holding in risky asset. In presence of a risk free asset and a risky asset following a Geometric Brownian motion, a continuous re-allocation as per the optimal holding leads to maximized wealth utility growth with predifined drawdown level almost surely.

$$
\begin{aligned}
X_t &= \dfrac{\mu}{\sigma^2} \dfrac{1}{(1 - \alpha)A + \alpha} (W_t - \alpha M_t) \\
Y_t &= \dfrac{\mu}{\sigma^2} \dfrac{1}{A} (W_t - K) \\
\end{aligned}
$$

There are still a few more gaps to fill to apply it in a portfolio management process.

Firstly we need to fit the one risky asset scenario assumed to the broad investable universe we are facing in the real world. One way, as mentioned at the very beginning of the blog, is to set the portfolio construction in two steps: determine the risky asset mix first and then set the leverage on the risky asset mix.  

Another way is to extend the optimal holding to support multi risky asset scenario as Cvitanic & Karatzas (1994) did. The optimal holding is still of the CPPI type. This exnapsion enables us to adjust allocation within asset classes or strategy components rather then take them as a whole. Obvisouly, this flexibility comes at a cost of more parameters to estimate.

$$
\begin{aligned}
X_t = \mu {(\sigma^{-1})}^2 \dfrac{1}{(1 - \alpha)A} (W_t - \alpha M_t) 1 \\
\end{aligned}
$$

In general, the incorporation of explicit control on drawdown as a regular portfolio manageemnt piece does not place additional burden on estimation. Current wealth level and previous peak wealth level are simply known and observable. As to expected performance and risk aversion, despite different assumption and faith we have, they are fundamental in a portfolio management process and should be there even wihout control on drawdown. 

It is quite natural to have the allocation of wealth into risky asset and risk free asset as the second step right after the construction of the asset mix. Either it is to build a risky asset mix as a whole or it is to build multiple risky assets in terms of asset classses, component strategies.





**The Parameter**


**The Discrete World**




Assuming that the risk asset follows a Geometric Brownian motion ($$dP_t = P_t((\mu + r) dt + \sigma dZ_t)$$), with $$X_t$$ amount of wealth ($$W_t$$) invested in risky asset and the remaining in riskless asset, we have the wealth following the stochastic process:

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

