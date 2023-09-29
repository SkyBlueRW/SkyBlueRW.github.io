#

## From Volatility to Maximum Drawdown


- [Introduction](#introduction)
- [Reference](#ref)

### Introduction <a name="introduction"></a>

Among the large group of risk mearues, volatility seems to be the one that raides the wave. And it is for good reasons. It roots deeply in the asset pricing theories linking closely to the concept of both risk and reward. It can be estimated and forecasted rather reliably in application. It bears nice analytical properties and can be extensively analyzed and efficeintly controlled in portfolio construction ...

The benefit of applying volatility to measure risk can goes on and on. While it is definitely not the perfect risk measure that summarizes all aspects of investment risk. It does not align well with how pepole would expect about risk in practice by recoganizing both unexpected loss and unexpected profit as risk, the latter is more likely to be called as "a nice surprise".






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
  
