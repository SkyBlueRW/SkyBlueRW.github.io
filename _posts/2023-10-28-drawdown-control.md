#

## Holding Discipline for Drawdown Control

- [Introduction](#introduction)
- [Optimal Holding with Drawdown Control](#optimal)
- [The Practical Side](#practice)
- [Reference](#ref)

### Introduction <a name="introduction"></a>

In the blog post [From Volatility to Maximum Drawdown](https://skybluerw.github.io/2023/10/15/max-drawdown.html), we delved into the widely acknowledged risk measure, maximum drawdown, looking into factors impacting it while uncovering pain points in its analysis and control in practice. Expanding upon this foundation, let's explore some practical approaches to incorporate drawdown management explicitly within a portfolio management process.

It's generally true that judgements about market conditions and strategies during pivotal moments play a paramount role in drawdown control. Often, a well-founded judgement regarding the efficacy of a strategy, even executed with rudimentary rule of thumbs in holding discipline, can shield investors reasonably from intolerable drawdowns.

Integrating an explicit control on drawdown into portfolio construction brings additional advantages, especially within a systematic portfolio management framework. It serves as a translator, converting judgments into a portfolio language consistent within the framework. It also facilitates ex-ante/post attribution, which is crucial for informed decision-making and continuous improvement. What's more, in scenarios where confident judgment is unavailable, the explicit incorporation enables us to fill the gap with backup plans grounded in clearly defined assumptions.

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

Despite the lenghty derivation, the optimal holding derived is quite intuitive of a type similar to Constant Proportion Portfolio Insurance(CPPI). By investing a constant proportion $$\dfrac{\mu}{\sigma^2} \dfrac{1}{(1 - \alpha)A + \alpha}$$ of the the maximum acceptable loss (difference between current wealth and lowest acceptable wealth level defined by prior peak $$W_t - \alpha M_t$$) invested in risky asset, we can maximize expected power utility growth while restricting maximum drawdown below ($$1 - \alpha$$) almost surely. 

Obviously, this downside protection comes at the cost of lower rate of wealth accumulation. When raising the maximum drawdown threshold from 0 to $$1 - \alpha$$, the expected log utility growth is scaled by $$1 - (1 + \dfrac{1-\alpha}{\alpha}A)^{-1}$$

This holding is consistent with our intuition for relavant factors about drawdown control. Larger 'safe cushion' above the threshold ($$W_t - \alpha M_t$$), better expected performance of the risky asset ($$\dfrac{\mu}{\sigma^2}$$), lower risk aversion (A) and higher acceptable maximum drawdown ($$1 - \alpha$$) safeguard higher allocation to the risky asset. It's also crucial to note that the optimality of this risky asset holding applies in the case of deterministic changing parameters of $$\mu$$ and $$\sigma$$. In such casese, the proportion would change as $$\mu$$ and $$\sigma$$ changes, allowing for much more flexible applications.

**Two Handy Variants**

This optimal holding can be further modified to variants that suit other use cases in drawdown management as well.

Firstly, it can be extended to the case of drawdown defined by absolute amount of wealth. In scenarios where investors aim to retain at least K dolloars, the optimal holding can be modified slightly to account it. Essentially it is equivalent to replace the constraint on floor from the stochastic $$M_t$$ to a constant K, leading to the safe cusion change from $$W_t - \alpha M_t$$ to $$W_t - K$$ and risk aversion adjustment from $$(1 - \alpha)A + \alpha$$ to $$A$$.

$$
\begin{aligned}
Y_t &= \dfrac{\mu}{\sigma^2} \dfrac{1}{A} (W_t - K) \\
\end{aligned}
$$

The holding based on one risky asset scenario discussed so far can be extended to multi risky assets scenario as done by Cvitanic & Karatzas (1994). Such expansion provides the flexibility to choose the granularity of risky asset classification. For instance, one can allocate funds within equities, bonds, and riskless assets or more specifically within large-cap equity, small-cap equity, government bonds, credit bonds, and money market instruments, all under the same framework with a constraint on drawdown. Such flexibility is would be quite helpful considering that our judgment may cover partially on the investment universe

$$
\begin{aligned}
X_t = \mu {(\sigma^{-1})}^2 \dfrac{1}{(1 - \alpha)A} (W_t - \alpha M_t) 1 \\
\end{aligned}
$$

### The practical Side <a name="practice"></a>

Here we are with a clearly defined optimal holding in risky asset. In the presence of one or a few risky assets following Geometric Brownian motion, a continuous re-allocation to these assets/portfolios as per the the optimal holding leads to maximized wealth utility growth with predifined drawdown level almost surely.

$$
\begin{aligned}
X_t &= \dfrac{\mu}{\sigma^2} \dfrac{1}{(1 - \alpha)A + \alpha} (W_t - \alpha M_t) \\
Y_t &= \dfrac{\mu}{\sigma^2} \dfrac{1}{A} (W_t - K) \\
\end{aligned}
$$

This optimal holding in the risky asset naturally fits into a two-step portfolio construction process, which involves building the portfolios of risky assets first and then determine the allocation within these risky portfolios and risk free asset as per the optimal holding in risky asset. Such a two-step process can be applied regularly during each rebalancing, in response to large deviations from the optimal risky holding, or in both scenarios.

The immediate question arises: how frequently should we rebalance, and what magnitude of deviation warrants a response? This tradeoff involves tolerances on breaking the maximum drawdown threshold, transaction costs, and return. On one hand, the optimality of the risky asset holding holds in the context of continuous allocation. More frequent rebalancing and smaller deviations to respond increase the likelihood of fulfilling the maximum drawdown threshold. Conversely, they result in higher transaction costs and lower holdings in the risky asset, leading to a loss in expected returns.

To address this tradeoff, insights from the perspective of contingent claims can be borrowed. You may already notice the similarities and links between this dynamic holding on risky asset and an option instrument on the same. It turns out that, entering into a call option with payoff of loss excessive of the maximum drawdown threshold ($$max(realized MDD - MDD threshold, 0)$$) provides similar protection against a predefined maximum drawdown threshold! Such an contigent claim is an exotic option with abundant analytical tools available out there.

For instance, Vercer (2006) simulated the delta exposure of this option given different maximum drawdown realized (MDD) and current realized drawdown (drawdown). Considering that a delta hedging portfolio of underlying can replicate this option that provides this drawdown protection, delta implies a dynamic portfolio that can attain the maximum drawdown threshold (Though wihout any consideration on the reward side), hence in some sense indicates the risk exposure to maximum drawdown. The value of the delta can offer another perspective on determining if our holding in risky assets deviates too far from the reference, independent from risk aversions and estimations on expected return.

![Gaussian](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/mdd_call_delta.png)

source: [Vecer (2006): Maximum Drawdown and Directional Trading](http://www.stat.columbia.edu/~vecer/maxdrawdown3.pdf)

Insights from the perspective of contingent claims extend beyond the delta plot alone. Meaningful insights can be gained from Gamma, the derivative of delta as well. Higher gamma indicates volatile exposures to maximum drawdown, suggesting more frequent rebalancing and a lower deviation range for the quickly changing exposure. Similar Monte Carlo simulations can help evaluate exposures to maximum drawdown in the form of delta and other Greeks under different circumstances of volatility, drift, big jumps, and more. It can provide a wealth of insights in addition to an optimized portfolio. For this purpose, numerous tools in the arsenal of derivative analysis become relevant through this angle.

It's also worth examining the parameters required for the calculation of this optimal holding. Among the components of the optimal holding, the drawdown threshold is predefined, and the current drawdown is observable. Regarding risk aversions, expected return, and volatility, they are standard inputs to a traditional Markowitz portfolio optimization. It seems plausible to add drawdown protection on top of a Markowitz-based portfolio management process without additional estimation tasks.

Choosing the same parameters for the two steps of the portfolio construction process is a legitimate option. However, there are cases where it may not be desirable or even possible. For the latter, numerous risk-centric portfolio construction models as we discussed in the ["The Conviction Pyramid of Portfolio Construction"](https://skybluerw.github.io/2023/04/01/pyramid-optimization.html) avoid estimating expected return due to its instability. For the former, there is indeed a reason to use different sources of estimation. Estimation errors themselves can lead to drawdown, and from a risk management perspective, it is reasonable to base the parameters for drawdown control on more conservative assumptions.

### Reference <a name="ref"></a>
- Grossman & Zhou (1993): Optimal Investment Strategies For Controlling Drawdowns
- Cvitanic & Karatzas (1994): On Portfolio Optimization Under "Drawdown" Constraints
- Vecer (2006): Maximum Drawdown and Directional Trading
- Busseti, Ryu & Boyd (2016): Risk-Constrained Kelly Gambling

