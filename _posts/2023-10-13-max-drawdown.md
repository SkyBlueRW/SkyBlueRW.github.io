#

## From Volatility to Maximum Drawdown


- [Introduction](#introduction)
- [Maximum Drawdown: The Way to Approach](#approach)
- [Maximum Drawdown Greek: A Simulation View](#factor)
- [Reference](#ref)

### Introduction <a name="introduction"></a>

Among the large group of risk mearues, volatility seems to be the one that rides the wave. And it is for good reasons. It roots deeply in the asset pricing theories linking closely to the concept of both risk and reward. It can be estimated and forecasted rather reliably in application. It bears nice analytical properties hence can be extensively analyzed and efficeintly controlled in portfolio construction ...

The benefit of using volatility to measure risk can go on and on. While volatility does not align exactly with how pepole view risk traditionally. It recoganize both abnormal loss and profit as risk, the latter of which is usually seen as "a nice surprise". 

Maximum Drawdown pops out in the case as one of the most popular risk measure focusing on downside of an investment. It is quoted in all kinds of investment reporting materials. Investors pay close attention to it as it represents the worst possible scenario one can encounter on an investment: buying at peak and exiting at trough.

In this blog, I'd like to kick off the discussion on maximum drawdown. The first section delves into ways to approch such a measure with rather poor analytical properties. Subsequently, we look into some pivotal factors influencing maximum drawdown via simulations, starting from the standard IID Gassuan and futher expanding to the 'wild world' of time dependence and non-Gaussian distribution. Many of the insights in the second section are drawn from the informative article [Van Hemert, Ganz, Harvey, Rattraym Martin & Yawitch (2020): Drawdowns](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3583864)


### Maximum Drawdown: The Approach <a name="approach"></a>

The definition and ex-post calculation of Maximum Dradwon ($$MDD_t$$) are unambiguous. Given the time series of net value on a strategy or security ($$P_t$$), we begin by identifying the peak ($$M_t$$) up to each point t and from there, it's straightforwad to calculate the drawdown ($$D_t$$) as the loss compared to that cumulative peak for each moment. The shapest drawdown observed is what we term as maximum drawdown.

$$
\begin{aligned}
M_t &= \max_{\mu \in [0, t]}{P_{\mu}} \\
DD_t &= \dfrac{P_t - M_t}{M_t} \\
MDD_t &= \min_{\mu \in [0, t]}{DD_{\mu}}
\end{aligned}
$$

It's evident that the characteristics of the return distribution, as well as the time dependence and the duration of return occurrences, are of great importance. A more extended investment horizon and a continuous string of losses are more likely to trigger severe drawdowns. The Maximum Drawdown is thus a random variable jointly determined by the stochastic return process and the investment horizon.

Ideally, we would derive the distribution of the Maximum Drawdown in terms of the return process and horizon, conduct a comprehensive study, and then use this knowledge for portfolio construction and risk management. Unfortunately, such a holistic approach is generally unfeasible for the Maximum Drawdown.

There is generally no closed-form solutions to describe this distribution. [Magdon-Ismail et al (2004)](https://www.jstor.org/stable/3215821?typeAccessWorkflow=login) derived the cumulative distribution function of Maximum Drawdown under the assumption that the net value of investment follows a Brownian motion with zero drift. However, even this cumulative distribution function, under quite ideal assumptions, is too complex for intuitive discussions or inclusion in portfolio optimization. Moreover, calculating the ex-ante Maximum Drawdown of a portfolio requires more than the Maximum Drawdown of each constituent; it calls for forecasting the return series for every constituent within the universe (N*T), an impractical endeavor.

Nevertheless, all hope is not lost. Despite these challenges, we can circle around and address Maximum Drawdown indirectly. For instance, during portfolio optimization, we can penalize other characteristics that tend to increase the magnitude of the Maximum Drawdown while being easier to incorporate, such as negative skewness or excessive kurtosis.

Additionally, while obtaining a closed-form function to describe the distribution of the Maximum Drawdown is elusive, designing investment policies to control it is comparatively more attainable. [Grossman & Zhou (1993)](https://onlinelibrary.wiley.com/doi/abs/10.1111/j.1467-9965.1993.tb00044.x) offered an optimal investment policy under Gaussian assumptions, allowing investors to achieve optimal expected utility growth with a hard constraint on Maximum Drawdown through dynamic adjustments in the holdings of risky assets.

To delve deeper into the practical application of these efforts, we must develop a more profound understanding of the Maximum Drawdown and the factors that influence it. This is precisely what we aim to explore through simulations in the next section.

### Maximum Drawdown Greek: A simualtion view <a name="factor"></a>

In absence of an analytical description on the distribution of maximum drawdown. We can swing the hammer of simulation to identify relavant return characteritics and determine the sensitivity of the probability of reaching a specific maximum drawdown level given these characteristics. As Van Hemert et al (2020), the return series of an 10 year investment with 0.5 Shapre and 10% volatility is used as the baseline case. Such monthly return is simulated 100,000 times for the empirical distribution of the maximum drawdown. 

On top of this basline case, we vary volatility, Shapre, time horizon, add time dependence and deviation in higher moments to measure the impact within and beyond IID Gaussian. The results are displayed in probabilities of breaching maximum drawdown of 1, 2, 3, 4 volatility for each case to show the sensitivity broadly. As shown below, lower sharpe ratio, longer investment horizon, higher auto-correlation in return/volatility and higher kurtosis would all raise the magnitude of the maximum drawdown.



**The 'Good Old' IID Gaussian**

![Gaussian](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/mdd_gaussian.png)

**The non-Gaussian Perspect**

![Moment](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/mdd_moment.png)

**The non-IID Perspective**

![Auto](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/mdd_tsc.png)

https://en.wikipedia.org/wiki/Edgeworth_series

**AR(1)**

$$
\begin{aligned}
r_t &= \mu + \sigma_t e_t \\
\sigma_t^2 &= \alpha_0 + \alpha_1 r_{t-1}^2\\
e_t &\sim N(0, 1) \\
\sigma^2 &= \dfrac{\alpha_0}{1-\alpha_1}
\end{aligned}
$$


**skew kurt**

$$
\begin{aligned}
Z_t &\sim N(0, 1) \\
r_t &= \mu + \sigma * Sinh((Arcsinh(Z_t) + skewness) * tailweight) * \dfrac{2}{Sinh(Arcsinh(2) * tailweight)}
\end{aligned}
$$


### Reference <a name="ref"></a>

- Van Hemert, Ganz, Harvey, Rattraym Martin & Yawitch (2020): Drawdowns
- Magdon-Ismail, Atiya, Pratap & Abu-Mostafa (2004): On the Maximum Drawdown of a Brownian Motion
- Grossman & Zhou (1993): Optimal Investmetn Strategies For Controlling Drawdowns
- Palomar's Slide on [Portfolio Optimization with Alternative Risk Measures](https://palomar.home.ece.ust.hk/MAFS5310_lectures/slides_CVaR_portfolio.html#1)
  
