#

## Holding Discipline for Drawdown Control

- [Introduction](#introduction)
- [Optimal Holding with Drawdown Control](#optimal)
- [The Practical Side](#practice)
- [Reference](#ref)

### Introduction <a name="introduction"></a>

In the blog post [From Volatility to Maximum Drawdown](https://skybluerw.github.io/2023/10/15/max-drawdown.html), we delved into the widely acknowledged risk measure, maximum drawdown, looking into factors impacting it while uncovering pain points in its analysis and control in practice. Expanding upon this foundation, let's explore some practical approaches to incorporate drawdown management explicitly within a portfolio management process.

It's generally true that judgements about market conditions and strategies during pivotal moments play a paramount role in drawdown control. Often, a well-founded judgement regarding the efficacy of a strategy, even executed with rudimentary rule of thumbs in holding discipline, can shield investors reasonably from intolerable drawdowns.

While integrating explicit drawdown control into portfolio construction brings additional advantages, especially within a systematic portfolio management framework. It serves as a translator, converting judgments into a portfolio language consistent across the entire framework. It also facilitates ex-ante/post attribution, which is crucial for informed decision-making and continuous improvement. What's more, in scenarios where confident judgment is unavailable, the explicit incorporation enables us to fill the gap with backup plans grounded in clearly defined assumptions.

With the benefits in mind, our focus in this blog turns to one such risky asset holding discipline initially introduced by Grossman & Zhou (1993). This discipline advocates for investing a constant proportion of the largest acceptable loss in risky assets to maximize expected utility growth within the desired drawdown range. The optimal holding derived from this approach can be used as a benchmark for determining the leverage of the risky asset mix, whether on a regular basis or in response to significant deviations.


### Optimal Holding with Drawdown Control <a name="optimal"></a>

Let's begin by taking a closer look at the discipline itself.

Assume $$W_t$$ represents for the value of wealth at time t and $$M_t$$ denotes the highest wealth level achieved before or at t. To explicitly manage drawdown level in portfolio construction, Grossman & Zhou (1993) introduced a hard constraint on maximum drawdown in the form of a stochastic floor determined by previous peak value ($$W_t \geq \alpha \mathop{Max}_{0\leq s\leq t}{W_s}$$, $$1 - \alpha$$ is the maximum acceptable drawdown). This constraint is imposed upon the classical portfolio optimization problem of maximizing the long term expected growth of power utility ($$U(W) = \dfrac{W^{1-A}}{1-A}$$). Accounting for different time values of current wealth and previous peak, we are essentially conducting the following portfolio optimization. ($$X_t$$ is the amount of money invested in the risky asset).

$$
\begin{aligned}
\mathop{Max}_{X_t} &
\mathop{lim}_{T\to \infty} \dfrac{1}{(1-A)T}lnE[(1-A)U(W_T)] \\
& P[W_t \geq \alpha e^{rt}\mathop{Max}_{0\leq s\leq t}(W^{\pi}_s e^{-rs}), 0\leq t\leq \infty] = 1 
\end{aligned}
$$

With time dynamics, probablistic expressions and expectations in it, the abovementioned portfolio optimization is definitely not easy to solve. Luckily, we stand on the shoulder of the giants :). Grossman & Zhou (1993) and Cvitanic & Karatzas (1994) solved the problem and derived the optiomal holding in risky asset analytically.

$$
\begin{aligned}
X_t &= \dfrac{\mu}{\sigma^2} \dfrac{1}{(1 - \alpha)A + \alpha} (W_t - \alpha M_t) \\
    &= \dfrac{\mu}{\sigma^2} \dfrac{1}{(1 - \alpha)A + \alpha} (1 - \alpha\dfrac{M_t}{W_t})W_t \\
M_t & = e^{rt}\mathop{Max}_{0\leq s\leq t}(W^{\pi}_s e^{-rs})
\end{aligned}
$$

Despite the lenghty derivation, the optimal holding derived is quite intuitive of the type similar to Constant Proportion Portfolio Insurance(CPPI). With a constant proportion $$\dfrac{\mu}{\sigma^2} \dfrac{1}{(1 - \alpha)A + \alpha}$$ of the the maximum acceptable loss (difference between current wealth and lowest acceptable wealth level defined by prior peak $$W_t - \alpha M_t$$) invested in risky asset, we can maximize expected power utility growth while restricting maximum drawdown below ($$1 - \alpha$$) almost surely. Obviously, this downside protection comes at the cost of lower rate of wealth accumulation. When raising the maximum drawdown threshold from 0 to $$1 - \alpha$$, the expected log utility growth is scaled by $$1 - (1 + \dfrac{1-\alpha}{\alpha}A)^{-1}$$

This holding is consistent with our intuition for drawdown control. Larger 'safe cushion' above the threshold ($$W_t - \alpha M_t$$), better expected performance of the risky asset ($$\dfrac{\mu}{\sigma^2}$$), lower risk aversion (A) and higher acceptable maximum drawdown ($$1 - \alpha$$) safeguard higher allocation to the risky asset. It's crucial to note that the optimality of this risky asset holding applies in the case of deterministic changing parameters of $$\mu$$ and $$\sigma$$. In such casese, the proportion would change as $$\mu$$ and $$\sigma$$ changes, allowing for much more flexible applications.

**Two Expansions**

What's quite handy is that this optimal holding can be modified to variants expanding to other uses cases in drawdown management as well.

Firstly, it can be extended to the case of drawdown defined by absolute amount of wealth. In scenarios where investors aim to retain at least K dolloars, the optimal holding can be modified slightly to account it. Essentially it is equivalent to replace the constraint on floor from the stochastic $$M_t$$ to a constant K, leading to the safe cusion change from $$W_t - \alpha M_t$$ to $$W_t - K$$ and risk aversion adjustment from $$(1 - \alpha)A + \alpha$$ to $$A$$.

$$
\begin{aligned}
Y_t &= \dfrac{\mu}{\sigma^2} \dfrac{1}{A} (W_t - K) \\
\end{aligned}
$$

What's also worth mentioning is that the one risky asset scenario discussed so far can be extended to multi risky assets as done by Cvitanic & Karatzas (1994). Such expansion provides the flexibility to choose the granularity of risky asset classification. For instance, one can allocate funds within equities, bonds, and riskless assets or more specifically within large-cap equity, small-cap equity, government bonds, credit bonds, and money market instruments, all under the same framework with a constraint on drawdown. Such flexibility is would be quite helpful considering that our judgment may cover partially on the investment universe

$$
\begin{aligned}
X_t = \mu {(\sigma^{-1})}^2 \dfrac{1}{(1 - \alpha)A} (W_t - \alpha M_t) 1 \\
\end{aligned}
$$

### The practical Side <a name="practice"></a>

Here we are with a clearly defined optimal holding in risky asset. In the presence of one or a few risky assets following Geometric Brownian motion, a continuous re-allocation as per the optimal holding leads to maximized wealth utility growth with predifined drawdown level almost surely.

$$
\begin{aligned}
X_t &= \dfrac{\mu}{\sigma^2} \dfrac{1}{(1 - \alpha)A + \alpha} (W_t - \alpha M_t) \\
Y_t &= \dfrac{\mu}{\sigma^2} \dfrac{1}{A} (W_t - K) \\
\end{aligned}
$$

Quite naturally, this optimal holding in risky asset can fit into a two-step portfolio construction process, which involves building the portfolio of risky assets first and then determine the allocation to this (or these) portfolio as per the holding derived. Looking into the values required for the calculation of this optimal holding, drawdown treshold is predefined; current drawdown is observable; As to risk aversions, expected return and volatility, they are the standard inputs to a traditional Markowitz portfolio optimization. Essentially, if the Markowtize optimization is used for portfolio construction, we can add down side protection on top of it wihout additional estimation job.

Now we can 

- natural way to apply it directly and regularly. no estimation
- only at large deriviation - option 
- one of the constraints.

There are still a few more gaps to fill to apply it in a portfolio management process. 

Firstly we need to fit the one risky asset scenario assumed to the broad investable universe we are facing in the real world. One way, as mentioned at the very beginning of the blog, is to set the portfolio construction in two steps: determine the risky asset mix first and then set the holding on the risky asset mix. In the sense, the optimal holding derived is used to restrict on the leverage of risky asset for the purpose of drawdown control. 

In general, the incorporation of explicit control on drawdown as a regular portfolio manageemnt piece does not place additional burden on estimation. Current wealth level and previous peak wealth level are simply known and observable. As to expected performance and risk aversion, despite different assumption and faith we have, they are fundamental in a portfolio management process and should be there even wihout control on drawdown. 

It is quite natural to have the allocation of wealth into risky asset and risk free asset as the second step right after the construction of the asset mix. Either it is to build a risky asset mix as a whole or it is to build multiple risky assets in terms of asset classses, component strategies.



Assume the existence of this risk free asset ($$rdt$$) and one risky asset ($$dP_t = P_t((\mu + r) dt + \sigma dZ_t)$$). With $$X_t$$ amount of wealth ($$W_t$$) invested in risky asset and the remaining in riskless asset, we have the wealth following the stochastic process:

$$
\begin{aligned}
dW_t &= X_t ((\mu + r) dt + \sigma dZ_t) + (W_t - X_t) r dt \\
     &= r W_t dt + X_t (\mu dt + \sigma dZ_t) \\
\end{aligned}
$$


### The Perspective of Contigent Claim <a name="perspective"></a>

You may already notice the similarities and links between this dynamic holding on risky asset and an option instrument on the same. It turns out that, entering into a call option with payoff of loss excessive of the maximum drawdown threshold ($$max(realized MDD - MDD threshold, 0)$$) provides similar protection against a predefined maximum drawdown threshold!

Vercer (2006) simulated the below delta exposure of this option given different maximum drawdown realized (MDD) and current realized drawdown (drawdown). Considering that a delta hedging portfolio of underlying can replicate this option that provides this drawdown protection. The delta itself implies a dynamic portfolio that can attain the maximum drawdown threshold (Though wihout any consideration on the reward side), hence providing a quantitative evaluation on current exposures to maximum drawdown.

![Gaussian](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/mdd_call_delta.png)

source: [Vecer (2006): Maximum Drawdown and Directional Trading](http://www.stat.columbia.edu/~vecer/maxdrawdown3.pdf)

This delta plot provides a consistent story as our optimal holding derived. At times when wealth is close to peak value or current drawdown is far from previous maximum drawdown, the delta exposure is close to zero. The delta grows nonlinearly as drawdown increases. Such a quantitative evaluation of exposure to maximum drawdown is definitely helpful for informed decision-making. It provides another angle focusing on drawdown itself free from risk aversion and considerations on profits. 

The insights we can obtain from the perspective of contigent claim is not restricted to this delta plot only. Similar Monte Carlo simulation can help to evaluate our exposures to maximum drawdown in the form of delta and other greeks under different circumstances of volatility, drift, big jumps and so on. It can provide us a lot more insights in addition to an optimized portfolio. For this purpose, a great deal of tools in the arsenal of derivative analysis become relavant via this angle.


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


Now we have a powerful tool that can help to harvest wealth appreciation within desired drawdown range. Definitely it is not the only approach to deal with drawdown risk. It deserves to take a quick detour to some other promising ways. These additional aspects help to a diversified view on the situation, and serve as great supplement to the optimal holding discipline we discussed or even fill in the place where it is not fitted. 

![Gaussian](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/mdd_call_delta.png)

source: [Vecer (2006): Maximum Drawdown and Directional Trading](http://www.stat.columbia.edu/~vecer/maxdrawdown3.pdf)

### Reference <a name="ref"></a>
- Grossman & Zhou (1993): Optimal Investment Strategies For Controlling Drawdowns
- Cvitanic & Karatzas (1994): On Portfolio Optimization Under "Drawdown" Constraints
- Vecer (2006): Maximum Drawdown and Directional Trading
- Busseti, Ryu & Boyd (2016): Risk-Constrained Kelly Gambling

