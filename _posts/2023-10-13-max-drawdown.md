#

## From Volatility to Maximum Drawdown


- [Introduction](#introduction)
- [Maximum Drawdown: The Way to Approach](#approach)
- [Maximum Drawdown Greek: A Simulation View](#factor)
- [Reference](#ref)

### Introduction <a name="introduction"></a>

Among the large group of risk mearues, volatility seems to be the one that rides the wave, with good reasons. It roots deeply in the asset pricing theories linking closely to the concept of both risk and reward. It can be estimated and forecasted rather reliably in application. It bears nice analytical properties hence can be extensively analyzed and efficeintly controlled in portfolio construction ...

The benefit of using volatility to measure risk can go on and on. While volatility does not align exactly with how pepole view risk traditionally. It recoganize both abnormal loss and profit as risk, the latter of which is usually seen as "a nice surprise". 

Maximum Drawdown pops out in the case as one of the most popular risk measures focusing on downside of an investment. Investors pay close attention to it as it represents the worst possible scenario one can encounter on an investment: buying at peak and exiting at trough. It is quoted in all kinds of investment reporting materials. 

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

It's evident that the characteristics of the return distribution, as well as the time dependence and the duration of return occurrences, are of great importance. A more extended investment horizon and a consecutive string of losses are more likely to trigger severe drawdowns. The Maximum Drawdown is thus a random variable jointly determined by the stochastic return process and the investment horizon.

Ideally, we would derive the distribution of the Maximum Drawdown in terms of the return process and horizon, conduct a comprehensive study, and then use this knowledge for portfolio construction and risk management. Unfortunately, such a holistic approach is generally unfeasible for the Maximum Drawdown.

There is generally no closed-form solutions to describe the distribution of Maximum Drawdown. [Magdon-Ismail et al (2004)](https://www.jstor.org/stable/3215821?typeAccessWorkflow=login) derived the cumulative distribution function of Maximum Drawdown under the assumption that the net value of investment follows a Brownian motion with zero drift. However, even this cumulative distribution function, under quite ideal assumptions, is too complex for intuitive discussions or inclusion in portfolio optimization. Moreover, calculating the ex-ante Maximum Drawdown of a portfolio requires more than the Maximum Drawdown of each constituent; it calls for forecasting the return series for every constituent within the universe (N*T), an impractical endeavor.

Nevertheless, the hope is not lost. Despite these challenges, we can circle around and address Maximum Drawdown indirectly. For instance, during portfolio optimization, we can penalize other characteristics that tend to increase the magnitude of the Maximum Drawdown while being easier to incorporate, such as negative skewness or excessive kurtosis.

Additionally, while obtaining a closed-form function to describe the distribution of the Maximum Drawdown is elusive, designing investment policies to control it is comparatively more attainable. [Grossman & Zhou (1993)](https://onlinelibrary.wiley.com/doi/abs/10.1111/j.1467-9965.1993.tb00044.x) offered an optimal investment policy under Gaussian assumptions, allowing investors to achieve optimal expected utility growth with a hard constraint on Maximum Drawdown through dynamic adjustments in the holdings of risky assets.

To delve deeper into the practical application of these efforts. We would appreciate to have some impressions about relavant factors and their impact on Maximum Drawdown. This is precisely what we aim to explore through simulations in the next section.

### Maximum Drawdown Greek: A simualtion view <a name="factor"></a>

In the absence of an analytical description of the Maximum Drawdown distribution, we turn to the tool of simulation. Swinging the hammer of simulation, we can get a sense ofhow the probability of reaching a specific Maximum Drawdown level is influenced by some key relavant attributes.

**Setting the Baseline**

Following Van Hemert et al. (2020), we start with a baseline return generation process with 0.5 Shapre and 10% volatility. Such monthly return of 10 years is simulated 100,000 times to build the empirical distribution of the maximum drawdown. The probabilities of breaching Maximum Drawdown thresholds of 1, 2, 3, and 4 multiples of volatility (corresponding to -10%, -20%, -30%, and -40% volatility) are found to be 97.%, 43%, 9.9%, and 1.5%, respectively.

Based on this baseline, we introduce variations in volatility, Sharpe ratio, time horizon, and incorporate time dependence, along with deviations in higher moments to assess their impact. We aim to get some sense on how these changes influence the probability of breaching Maximum Drawdown thresholds of 1, 2, 3, and 4 sigmas. As we delve into the details below, we discover that a lower Sharpe ratio, an extended investment horizon, higher auto-correlation in returns and volatility, and increased kurtosis all contribute to larger Maximum Drawdowns.


**The 'Good Old' IID Gaussian**

Starting with the 'Good Old World' of IID Gaussian where mean and variance are the sole architects of return generation. Here, only three factors impact Maximum Drawdown: mean, variance, and investment horizon. In the three charts below, we explore the effect of changing volatility, Sharpe ratio (as a measure of mean), or time horizon while keeping the other two constant.

One intriguing observation is that when we express Maximum Drawdown thresholds as multiples of volatility, changes in volatility have almost no impact on the probabilities of breaching these thresholds. The slight downward slope can be attributed to the compounding nature of return aggregation. This suggests that imposing constraints on volatility alone can effectively limit Maximum Drawdown in the IID Gaussian scenario, also justify Van Hermer et al.'s (2020) choice to express Maximum Drawdown thresholds as multiples of volatility.

On the other hand, it's no surprise to see that probabilities of breaching Maximum Drawdown thresholds increase as Sharpe ratio decreases or investment horizon lengthens.


![Gaussian](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/mdd_gaussian.png)

**Higher Moments**

In reality, it's quite rare to encounter an investment whose returns follow the IID Gaussian. In most cases, we expect some degree of deviation in terms of distribution or time dependence. To emulate these differences in higher moments of the distribution, we employ the Gram-Charlier expansion to introduce skewness and kurtosis deviations to the baseline case, examining their impact on Maximum Drawdown.

To ensure a well-defined distribution, we vary skewness from -0.3 to 0.3 and excess kurtosis from 0 to 6, aligning the mean and variance with the baseline case for a fair comparison. Within this range, changes in skewness don't significantly impact Maximum Drawdown, whereas increases in kurtosis lead to a substantial rise in Maximum Drawdown. However, this doesn't imply that skewness doesn't influence Maximum Drawdown. Our simulations are restricted to a relatively narrow range, making it challenging to explore the full range of skewness's impact.

![Moment](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/mdd_moment.png)

**Time Dependence**

Last but certainly not least, we introduce time dependence to return and local volatility in the baseline case.

Specifically, we simulate returns with auto-correlation ranging from -0.5 to 0.5 using the following formula, where the parameter $$\rho$$ represents the auto-correlation added. As shown in the first chart below, increasing the auto-correlation corresponds to an increase in the probabilities of reaching corresponding Maximum Drawdown thresholds.

$$
r_t = (1-\rho) \mu + \rho r_{t-1} + \sqrt{1 - \rho ^ 2} \sigma
$$

To replicate the volatility clustering seen in many asset classes, we use an ARCH(1) process. The larger the parameter $$alpha_1$$, the more volatility clustering we introduce. Similarly, we observe an increase in probabilities with greater volatility clustering.

$$
\begin{aligned}
r_t &= \mu + \sigma_t e_t \\
\sigma_t^2 &= \alpha_0 + \alpha_1 r_{t-1}^2\\
e_t &\sim N(0, 1) \\
\sigma^2 &= \dfrac{\alpha_0}{1-\alpha_1}
\end{aligned}
$$

![Auto](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/mdd_tsc.png)






sum

take as much insights from IID Gaussian and be aware of ...

### Reference <a name="ref"></a>

- Van Hemert, Ganz, Harvey, Rattraym Martin & Yawitch (2020): Drawdowns
- Magdon-Ismail, Atiya, Pratap & Abu-Mostafa (2004): On the Maximum Drawdown of a Brownian Motion
- Grossman & Zhou (1993): Optimal Investmetn Strategies For Controlling Drawdowns
- Palomar's Slide on [Portfolio Optimization with Alternative Risk Measures](https://palomar.home.ece.ust.hk/MAFS5310_lectures/slides_CVaR_portfolio.html#1)
  
