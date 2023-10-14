#

## From Volatility to Maximum Drawdown


- [Introduction](#introduction)
- [Maximum Drawdown: The Way to Approach](#approach)
- [Maximum Drawdown Greek: A Simulation View](#factor)
- [Reference](#ref)

### Introduction <a name="introduction"></a>

Among the large group of risk mearues, volatility seems to be the one that rides the wave. And it is for good reasons. It roots deeply in the asset pricing theories linking closely to the concept of both risk and reward. It can be estimated and forecasted rather reliably in application. It bears nice analytical properties and can be extensively analyzed and efficeintly controlled in portfolio construction ...

The benefit of using volatility to measure risk can go on and on. While volatility does not align exactly with how pepole view risk traditionally. It recoganize both abnormal loss and profit as risk, the latter of which is usually seen as "a nice surprise". 

Maximum Drawdown pop out in the case as one of the most popular risk measure focusing on downside of an investment. It is quoted in all kinds of investment reporting materials. Investors pay close attention to it as it represents the worst possible scenario one can encounter on an investment: buy at peak and exit at trough.

In this blog, I'd like to kick off the discussion on maximum drawdown. The first section would be devoted to ways to approch such a measure with rather poor analytical properties. In the following section, we will look into some key driving factors impacting maximum drawdown, starting from the standard IID Gassuan and futher expanding to the 'wild world' of time dependence and non-Gaussian distribution. Lots of the settings in the simulation of 2nd section are from the informative article [Van Hemert, Ganz, Harvey, Rattraym Martin & Yawitch (2020): Drawdowns](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3583864)

### Maximum Drawdown: The Approach <a name="approach"></a>

The definition and ex-post calculation of Maximum Dradwon ($$MDD_t$$) is unambigious. Given the time series of net value on a strategy/security ($$P_t$$), we can firstly identify the peak ($$M_t$$) up to the point t and then easily calculate the drawdown ($$D_t$$) as the loss compared to that cumulative peak for each moment. The shapest drawdown has ever happend is the Maximum Drawdown.

$$
\begin{aligned}
M_t &= \max_{\mu \in [0, t]}{P_{\mu}} \\
DD_t &= \dfrac{P_t - M_t}{M_t} \\
MDD_t &= \min_{\mu \in [0, t]}{DD_{\mu}}
\end{aligned}
$$

Clearly, not only the return distribution but also the time dependece and length of the return occurence matter. Longer investment horizon is more likely to trigger more severe drawdown, as is a stream of continous loss. We would expect maximum drawdown is a random variable jointly determined by the stochastic process of the return and the investment horizon. 

Ideally, we should derive the distribution of the maximum drawdown in terms of the return process and horizon, study this distribution thoroughly and restrict it within acceptable range with this knowledge in portfolio construction and risk management. Unfortunately, this comprehensive approach is generally not viable for maximum drawdown. 

There is generally no closed form solutions to describe this distribution. [Magdon-Ismail et al (2004)](https://www.jstor.org/stable/3215821?typeAccessWorkflow=login) derived the cumulative distribution function of maximum drawdown under the assumption that the net value of investment follows a Brownian motion with zero drift. While even this CDF function under quite ideal assumptions is too complex to proceed with further intuitive discussions or incorporation in portfolio optimization. Additionally, the maximum drawdown of a portfolio takes more than maximum drawdown of each constituent to aggregate. To control the maximum drawdown explicitly in a portfolio constuction process, we need to forecast the return series for every constituent within the universe (N*T), which is obviously not realistic. 

While defintely it is not a desperate battle. With all these challenges we might try to circle around and tackle the maximum drawdown indirectly. 

For example, during the portfolio optimization, we can penalize other characteristics likely raising the magnitude of maximum drawdown at the same time much easier to incorporate (such as negative skewness, excessive kurtosis, etc...). Additionaly, though it is hard to get a closed form function to desrcibe the distribution of maximum drawdown, it is comparably easier to design a risky investment policies to have maximum drawdown under control. [Grossman & Zhou (1993)](https://onlinelibrary.wiley.com/doi/abs/10.1111/j.1467-9965.1993.tb00044.x) provides the optimal investment policy under the Gaussian assumption. Such an investment policy enables investors to achieve optimal expected utility growth with hard constraint on maximum drawdown via dynamic adjustment on holding of risky assets. 

To further elaborate this srategy for practical application, we need to get more sense about maximum drawdown. We need to know more about what factors impact the maximum drawdown in what way. That's what we are gonna to dig a little bit with simulation in the next section.


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
  
