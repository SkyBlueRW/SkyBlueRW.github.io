#

## From Volatility to Maximum Drawdown


- [Introduction](#introduction)
- [Maximum Drawdown: The Approach](#approach)
- [MDD Greek: A Simulation View](#factor)
- [Reference](#ref)

### Introduction <a name="introduction"></a>

Among the large group of risk mearues, volatility seems to be the one that rides the wave. And it is for good reasons. It roots deeply in the asset pricing theories linking closely to the concept of both risk and reward. It can be estimated and forecasted rather reliably in application. It bears nice analytical properties and can be extensively analyzed and efficeintly controlled in portfolio construction ...

The benefit of using volatility to measure risk can goes on and on. While volatility does not align exactly with how pepole view risk traditionally. It recoganize both unexpected loss and unexpected profit as risk, the latter of which is usually seen as "a nice surprise". 

Maximum Drawdown pop out in the case as one of the most popular used risk measure focusing on downside of an investment. Investors pay close attention to maximum drawdown with all kinds of investment reporting materials quoting it.

In this blog, I'd like to kick off the discussion on this metric. The first section would be devoted to ways to approch such measure with rather poor analytical properties. In the following section, we will look into some key driving factors impacting maximum drawdown, starting from the standard IID Gassuan and futher expanding to the 'wild world' of time dependence and non-Gaussian distribution. Lots of the settings in the simulation of section 2 are from this wonderful article [Van Hemert, Ganz, Harvey, Rattraym Martin & Yawitch (2020): Drawdowns](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3583864)

### Maximum Drawdown: The Approach <a name="approach"></a>

The calculation of Maximum Dradwon ($$MDD_t$$) is unambigious. Given the time series net value of a strategy/security ($$P_t$$), we can firstly identify the cumulative peak ($$M_t$$) and then easily calculate the drawdown ($$D_t$$) as the loss compared to that cumulative peak for each moment . The shapest drawdown has ever happend is the Maximum Drawdown.


$$
\begin{aligned}
M_t &= \max_{\mu \in [0, t]}{P_{\mu}} \\
DD_t &= \dfrac{P_t - M_t}{M_t} \\
MDD_t &= \min_{\mu \in [0, t]}{DD_{\mu}}
\end{aligned}
$$

Clearly the order of the return

hard to combine 
hence the drawdown ($$DD_t$$) for each time on the investment (P). The sharpest drawdown ever happend is the Maximum Drawdown.

What poses challenges is that maximum drawdown does not really bear nice analytical properties. Other than return distribution, the sequence of the realized return also matters! Accounting for this time dependence nature, we would expect maximum drawdown is a random variable jointly governned by return distribution and investment horizon. 

There is generally no closed form  solutions to describe the distribution of maximum drawdown even with the return distribution and investment horizon clearly defined. Magdon-Ismail et al (2004) derived the cumulative distribution function of MDD under the assumption that the net value of investment follows Brownian motion with zero drift. While even this result under a quite ideal assumption is too complex to proceed with further intuitive discussions.


**Bottom Up**

**Top Down**


worst case scenario: buying at peak and selling at bottom

extremely sensitive. Normal distribution -> distribution of drawdown is function of variance. Effective handling of MDD with constraits on volatility itself. 

penalize negative skew and positive kurtosis




![Gaussian](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/mdd_gaussian.png)


![Moment](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/mdd_moment.png)


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
- Palomar's Slide on [Portfolio Optimization with Alternative Risk Measures](https://palomar.home.ece.ust.hk/MAFS5310_lectures/slides_CVaR_portfolio.html#1)
  
