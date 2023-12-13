#

## Risk discipline for Drawdown Control

- [Introduction](#introduction)
- [Optimal Holding for Drawdown Control](#optimal)
- [The Practical Side](#practice)
- [Reference](#ref)

### Introduction <a name="introduction"></a>


As discussed in a previous blog [From Volatility to Maximum Drawdown](https://skybluerw.github.io/2023/10/15/max-drawdown.html), maximum drawdown, though attracts significant attention for the evaluation of investments, is not obvious to analyze or control in practice. Following on the previous discussion on factors closly linked to the maximum drawdown, we will explore some viable ways to incorporate controls on drawdown risk explicitly in the portfolio management process. 

It's probably true that judgements of market condition and strategies at critical moments are what matter the most for the control of drawdown risk. In a lot of times, reasonable judgement about efficacy of strategy can protect investors reasonably well from unberable drawdown even with basic rule of thumbs in holding control. While the explict incorporation of drawdown control into portfolio construction bears additional merits, especially from the perspective of a systematic portfolio construction process. It helps to translate any judgement we have to a consistent portfolio languange, it facilitate ex-post attribution that are important to summarize hence improve, and it provides ways to fill in the gap in case strong judgement is not available.

In this blog, let's look into the discipline of risky asset holding that Grossman & Zhou (1993) initially proposed for the aim. A constant proportion of the largest acceptable loss can be invested on risky assets to achieve largest expected utility growth while fulffilling drawdown threshold. The discipline generally does not place additional burden of estimation. Traditional inputs to the Markowitz optimization like expected return and risk along with risk aversion are required for the calculation. Such an optimal holding in risky asset can be used as a reference to determine the leverage/holding of risky asset mix, either regularly or in case of large deviation happens.

### Optimal Holding for Drawdown Control <a name="optimal"></a>

Let's firstly have a look at the discipline itself for what it is. 

Suppose $$W_t$$ stands for the value of wealth at t and $$M_t$$ stands for the higest ever wealth level achieved prior to t. To incorporate drawdown control in portfolio construction explicitly, Grossman & Zhou (1993) added a hard constraint on maximum drawdown in the form of a stochastic floor determined by previous peak value ($$W_t \geq \alpha \mathop{Max}_{0\leq s\leq t}{W_s}$$, $$1 - \alpha$$ is the maximum acceptable drawdown) upon the classical portfolio optimization problem of maximizing the long term expected growth of power utility ($$U(W) = \dfrac{W^{1-A}}{1-A}$$). With different time value accounted for current wealth and previous peak value, we are essentially conducting the following portfolio optimization. ($$X_t$$ is the amount of money invested in the risky asset).

$$
\begin{aligned}
\mathop{Max}_{X_t} &
\mathop{lim}_{T\to \infty} \dfrac{1}{(1-A)T}lnE[(1-A)U(W_T)] \\
& P[W_t \geq \alpha e^{rt}\mathop{Max}_{0\leq s\leq t}(W^{\pi}_s e^{-rs}), 0\leq t\leq \infty] = 1 
\end{aligned}
$$

The abovementioned portfolio optimization is definitely not easy to solve. Luckily we are standing on the shoulder of the giants :) Grossman & Zhou (1993) and Cvitanic & Karatzas (1994) solved the problem and derived the optiomal holding in risky asset analytically.

$$
\begin{aligned}
X_t &= \dfrac{\mu}{\sigma^2} \dfrac{1}{(1 - \alpha)A + \alpha} (W_t - \alpha M_t) \\
    &= \dfrac{\mu}{\sigma^2} \dfrac{1}{(1 - \alpha)A + \alpha} (1 - \alpha\dfrac{M_t}{W_t})W_t \\
M_t & = e^{rt}\mathop{Max}_{0\leq s\leq t}(W^{\pi}_s e^{-rs})
\end{aligned}
$$

Despite the lenghty derivation, the optimal holding is quite intuitive of the Constant Proportion Portfolio Insurance(CPPI) type. With a constant proportion $$\dfrac{\mu}{\sigma^2} \dfrac{1}{(1 - \alpha)A + \alpha}$$ of the the maximum acceptable loss (difference between current wealth and lowest acceptable wealth level defined by prior peak $$W_t - \alpha M_t$$) invested in risky asset, we can maximize expected power utility growth while restricting maximum drawdown below ($$1 - \alpha$$) almost surely. Obviously, this downside protection is at a cost of lower rate of wealth accumulation. When we raise the largest acceptable maximum drawdown from 0 to $$1 - \alpha$$, the expected log utility growth is scaled by $$1 - (1 + \dfrac{1-\alpha}{\alpha}A)^{-1}$$

Looking into the optiomal holding in more details, larger 'safe cushion' above the floor ($$W_t - \alpha M_t$$), better expected performance of the risky asset ($$\dfrac{\mu}{\sigma^2}$$), lower risk aversion (A) and higher acceptable maximum drawdown ($$1 - \alpha$$) safeguard higher allocation to the risky asset. It should be noted that the optimality of holding pertains in case of deterministic changing paramters of $$\mu$$ and $$\sigma$$, which enables a lot more ways to put it in practice.

It can be extend to the case where investors want to refrain from drawdown dragging the wealth value below a constant treshold K as well. The resulting optimal holding is still in the form of CPPI like. Essentially it is equivalent to replace the stochastic floor from the maximum drawdown to a constant k leading to the safe cusion changing from $$W_t - \alpha M_t$$ to $$W_t - K$$ and risk aversion adjustment from $$(1 - \alpha)A + \alpha$$ to $$A$$.

$$
\begin{aligned}
Y_t &= \dfrac{\mu}{\sigma^2} \dfrac{1}{A} (W_t - K) \\
\end{aligned}
$$

 


### The practical Side <a name="practice"></a>

Here we are with a clearly defined optimal holding in risky asset. In presence of a risk free asset and a risky asset following a Geometric Brownian motion, a continuous re-allocation as per the optimal holding leads to maximized wealth utility growth with predifined drawdown level almost surely.

$$
\begin{aligned}
X_t &= \dfrac{\mu}{\sigma^2} \dfrac{1}{(1 - \alpha)A + \alpha} (W_t - \alpha M_t) \\
Y_t &= \dfrac{\mu}{\sigma^2} \dfrac{1}{A} (W_t - K) \\
\end{aligned}
$$

There are still a few more gaps to fill to apply it in a portfolio management process.

Firstly we need to fit the one risky asset scenario assumed to the broad investable universe we are facing in the real world. One way, as mentioned at the very beginning of the blog, is to set the portfolio construction in two steps: determine the risky asset mix first and then set the holding on the risky asset mix. In the sense, the optimal holding derived is used to restrict on the leverage of risky asset for the purpose of drawdown control. 

It is worth mentioning that the one risky asset scenario can be extended to multi risky assets as Cvitanic & Karatzas (1994) did. The optimal holding is still of the CPPI type. This exnapsion enables us to adjust allocation within risky asset as well. 

$$
\begin{aligned}
X_t = \mu {(\sigma^{-1})}^2 \dfrac{1}{(1 - \alpha)A} (W_t - \alpha M_t) 1 \\
\end{aligned}
$$

In general, the incorporation of explicit control on drawdown as a regular portfolio manageemnt piece does not place additional burden on estimation. Current wealth level and previous peak wealth level are simply known and observable. As to expected performance and risk aversion, despite different assumption and faith we have, they are fundamental in a portfolio management process and should be there even wihout control on drawdown. 

It is quite natural to have the allocation of wealth into risky asset and risk free asset as the second step right after the construction of the asset mix. Either it is to build a risky asset mix as a whole or it is to build multiple risky assets in terms of asset classses, component strategies.





**The Parameter**


**The Discrete World**


Assume the existence of this risk free asset ($$rdt$$) and one risky asset ($$dP_t = P_t((\mu + r) dt + \sigma dZ_t)$$). With $$X_t$$ amount of wealth ($$W_t$$) invested in risky asset and the remaining in riskless asset, we have the wealth following the stochastic process:

$$
\begin{aligned}
dW_t &= X_t ((\mu + r) dt + \sigma dZ_t) + (W_t - X_t) r dt \\
     &= r W_t dt + X_t (\mu dt + \sigma dZ_t) \\
\end{aligned}
$$



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

