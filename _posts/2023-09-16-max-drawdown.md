#

## From Volatility to Maximum Drawdown


- [Introduction](#introduction)
- [Reference](#ref)

worst case scenario: buying at peak and selling at bottom

extremely sensitive. Normal distribution -> distribution of drawdown is function of variance. Effective handling of MDD with constraits on volatility itself. 

penalize negative skew and positive kurtosis


### Introduction <a name="introduction"></a>


![Gaussian](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/mdd_gaussian.png)


**AR(1)**

$$
\begin{aligned}
r_t &= \mu + \sigma_t e_t \\
\sigma_t^2 &= \alpha_0 + \alpha_1 r_{t-1}^2\\
e_t &\sim N(0, 1) \\
\sigma^2 &= \dfrac{\alpha_0}{1-\alpha_1}
\end{aligned}
$$


### Reference <a name="ref"></a>

- Jones & Pewsey (2009): Sinh-arcsinh distributions
- Magdon-Ismail, Atiya, Pratap & Abu-Mostafa (2004): On the Maximum Drawdown of a Brownian Motion
